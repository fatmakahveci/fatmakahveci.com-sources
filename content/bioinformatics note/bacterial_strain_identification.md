---
title: Bacterial Strain Identification
description: Here is an intro to bacterial strain identification.
summary: "Here is an intro to bacterial strain identification."
date: 17-11-2022
categories:
  - "Bioinformatics"
tags:
  - "bacterial strain identification"
  - "bacteria"
  - "strain"
  - "bioinformatics"
comments: true
---
Bacterial species are highly adaptable to their environment in harsh conditions. It makes bacterial infections of great concern due to their relevance to the high mortality, morbidity rates, and cost of treatments. It is critical to discriminate bacterial isolates at the strain level in transmission surveillance during infectious disease outbreaks.

WGS-based approaches pave the way to identify and characterize bacterial species and strains. It is feasible with increasing available data size and ease of their applicability through SNVs among strains, as a group of closely related isolates that share critical characteristics. SNVs in the core genome are a good starting point for discrimination in case the aim is distantly related organisms.

Alignment-based approaches successfully investigate the evolution of members from the same strain. However, the poor representation of a species' genome, impacting read mapping and introducing bias, prevents having a good-quality reference. No gold standard reference genome is available for bacterial species because of their ever-changing genomic characteristics. As genes are generally the unit of selection, treating them as discrete units of analysis is valid.

As a strain identification approach, multilocus sequence typing (MLST) has become the fundamental bacterial classification technique. It associates an isolate to a sequence type defined by a specific allelic profile based on an established MLST schema. However, traditional MLST schemas could not discriminate separate strains within a clonal complex of Neisseria meningitidis. It emerged MLST schemas consisting of more genes. In this regard, we use core gene MLST schemas, comprised of the set of core genes shared by a group of related strains, generally relying on a few hundred genes, covering most of the loci of the considered strains. Although the core genome covers only a tiny amount of the whole genome, it provides a robust and informative way for identification.

A data-specific core reference genome overcomes the poor reference problem. A core genome is the part of the whole genome containing conserved genes common in all strain samples. It consists of genes shared by more than 95\% of all strains among the individuals of a bacterial species. The remaining is due to sequencing coverage problems, assembly problems, or other issues related to draft genome assembly usage.

The increase in sequenced genomes makes it difficult to handle multiple genomes at the required scale. To solve this problem, we need both cost- and time-efficient approaches. Comparison of highly variable loci in different individuals achieves accurate identification at the strain level. Also, WGS-based bacterial typing can be applied to many bacterial isolates of any species simultaneously with no need for the organism- or target-specific reagents. The results will be informative for both routine surveillance and outbreak investigation. We can compare the previous and current analyses and share the ultimate results. Moreover, they are less biased compared to the traditional culture- and assay-based approaches because they do not require any a priori knowledge of the sample composition.

Read alignment to large genomic databases, read-mapping to a chosen reference, and statistical/probabilistic analysis methods can identify the strains. Mapping-based approaches are more common because alignment-based ones are not always applicable due to the amount of data and resource requirements. The mapping-based methods may use kmer libraries, marker genes, or whole genome references.

---

Updated by *Fatma* on November 17, 2022
