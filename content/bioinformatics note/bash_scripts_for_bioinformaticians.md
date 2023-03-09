---
title: Bash scripts for bioinformaticians
description: Bash scripts for bioinformaticians
summary: "Bash scripts for bioinformaticians"
date: 15-06-2020
categories:
  - "Bioinformatics"
tags:
  - "bioinformatician"
  - "bioinformatics"
  - "bash"
---

- Split a single fasta file into multiple fasta files.

```bash
#!/bin/bash

echo "usage: ./split_single_to_multiple_fasta.sh inputFile.fasta"

inputFile=$1

cat $1 | awk '{ if (substr($0, 1, 1)==">") {filename=(substr($0,2) ".fa")} print $0 > filename }'
```

#### Data preprocessing

- Download paired-end sequencing data
  - [SRA-tools installation](https://ncbi.github.io/sra-tools/install_config.html)
  - Run `fastq-dump [--outdir ${outputDirectory}] [--gzip] -I --split-files ${sampleID}`
- [AdapterRemoval](https://github.com/MikkelSchubert/adapterremoval) searches for and removes adapter sequences from High-Throughput Sequencing (HTS) data and (optionally) trims low quality bases from the 3' end of reads following adapter removal. AdapterRemoval can analyze both single end and paired end data, and can be used to merge overlapping paired-ended reads into (longer) consensus sequences. Additionally, AdapterRemoval can construct a consensus adapter sequence for paired-ended reads, if which this information is not available.

#### Filtering and manipulating bam files

- [picard](https://broadinstitute.github.io/picard/)

#### Integrative Genomic Viewer

- [IGV](http://software.broadinstitute.org/software/igv/)

#### Metagenomics screening of shotgun data

- [Mentalist](https://github.com/fatmakahveci/mentalist)

#### Reads alignment and variants calling

- [bwa]( https://github.com/lh3/bwa)
- [gatk](https://software.broadinstitute.org/gatk/)
- [samtools](http://www.htslib.org/doc/samtools.html)
- [bcftools](http://samtools.github.io/bcftools/bcftools.html)

```bash
#!/usr/bin/env nextflow

process < name > {

   [ directives ]

   input:
    < process inputs >

   output:
    < process outputs >

   when:
    < condition >

   [script|shell|exec]:
   < user script to be executed >

}
```

[http://www.metagenomics.wiki/tools/samtools](http://www.metagenomics.wiki/tools/samtools)

## Download and install

`wget https://github.com/samtools/samtools/releases/download/*1.3.1*/samtools-*1.3.1*.tar.bz2`
`tar -jvxf samtools-*1.3.1*.tar.bz2`
`cd samtools-*1.3.1*`
`make`
`make prefix=*$HOME/tools/samtools* install`  # path where to install samtools

- Add path to your .bashrc file

```bash
export PATH=*$HOME/tools/samtools*/bin/:$PATH
```

[http://www.htslib.org/download/](http://www.htslib.org/download/)

## Examples

- Convert a SAM file to a BAM file

`samtools **view -b -S** *SAMPLE*.sam > *SAMPLE*.bam`
 `-S` Input is in SAM format
 `-b` Output in BAM format
**
\*convert a BAM file to a SAM file\***
`samtools **view -h** *SAMPLE*.bam > *SAMPLE*.sam`
**
\*sort a BAM file\***

```bash
samtools **sort** *SAMPLE*.bam **-o \*SAMPLE\*_sorted.bam**
```

- Using a unix pipe (input '-')

```bash
cat *SAMPLE*.bam **|** samtools sort **-** -o *SAMPLE*_sorted.bam
```

~~`samtools **sort** *SAMPLE*.bam *SAMPLE*`~~  *# old version v1.2*

***sort by readName\***
`samtools **sort -n** *SAMPLE*.bam -o *SAMPLE*_sorted.bam`

## Stats

***get number of alignments\***
`samtools **view -c** *SAMPLE*.bam`
**
\*more statistics about alignments\***
`samtools **flagstat** *SAMPLE*.bam`
**
\*comprehensive statistics\***
`samtools **stats** *SAMPLE*.bam`

## Get coverage

***# get coverage of a selected region** (e.g., from base 1,958,700 to 1,958,907 of a contig)*
`samtools **index** sampleID.bam`
`samtools **mpileup -r** 'contigName:1,958,700-1,958,907' sampleID.bam`
*# same in combination with [awk](http://www.metagenomics.wiki/tools/ubuntu-linux/awk) to count the total and averaged coverage*
`samtools **mpileup** -r 'contigName:``1,958,700-1,958,907' sampleID.bam | **awk** 'BEGIN{C=0}; {C=C+$4}; END{``print C "\t" C/NR}'`

see also: [→ Calling SNPs/INDELs with SAMtools/BCFtools](http://samtools.sourceforge.net/mpileup.shtml)

Note: SAMtools mpileup counts only primary aligned reads. SAMtools discards unmapped reads, secondary alignments and duplicates. To consider also secondary alignments, [BEDtools](http://bedtools.readthedocs.org/en/latest/content/tools/coverage.html) could be an alternative.

## SAMtools documentation

[Samtools homepage](http://www.htslib.org/)

[Samtools documentation](http://www.htslib.org/doc/samtools.html)

[Introduction by Dave Tang](http://davetang.org/wiki/tiki-index.php?page=SAMTools)

## Alternative BAM processing tools

[→ Sambamba](http://lomereiter.github.io/sambamba/)

[→ BEDtools](http://bedtools.readthedocs.io/en/latest/content/tools/coverage.html)
