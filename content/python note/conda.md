---
title: Conda
description: Conda
summary: "Updated by Fatma, Mar 28, 2023."
date: 28-03-2023
categories:
  - "Coding"
tags:
  - "Python"
  - "coding"
  - "algorithms"
  - "data structures"
comments: true
---
- It is a package, dependency, and environment management.
- It was created for Python, but it is also used for R, Java, C/C++, etc.
- It runs on macOS, Linux, etc.
- If you need a package that requires another version of Python, use `conda`.
- Use the most recent version.

## miniconda vs. anaconda

### miniconda

- Choose if you are a newbie to python and have the time and disk space.

- Install 1,500 scientific packages automatically installed __at once__.

- Every time you open up a terminal, `conda` won’t automatically be available. Run the command below to use `conda` within `miniconda`.

> export PATH=$HOME/miniconda/bin:$PATH

### anaconda

- Install each package separately.

## Installation

- [macOS](https://docs.anaconda.com/anaconda/install/mac-os/)
- [Linux](https://docs.anaconda.com/anaconda/install/linux/)
- [Docker](https://hub.docker.com/u/continuumio)

### Update packages

`> conda update conda`

- It is friendly with _pip_. It means that if you can't find a package in Anaconda Cloud, you can install it using _pip_.

## Creating a `conda` environment

- There are two ways of creating a `conda` environment.

### 1. An environment file in YAML

- __YAML :=__ YAML Ain't Markup Language

environment.yml

```yaml
name: <environment_name>
channels:
- conda-forge
dependencies:
- python=<python_version>
- pip
- pip:
    - <pip_package_name>
```

- To create an environment:

`> conda env create --file <environment.yml>`

### 2. Manual specification of packages

`> conda create -c conda-forge -n <environment_name> python=<python_version> <pip_package_name_1> <pip_package_name_2> <...>`

- conda env remove -n live_env

- To activate an environment:

`> conda activate <environment_name>`

- To deactivate an environment:

`> conda deactivate`

- To delete an environment:

`> conda env remove -n <environment_name>`

- To see the packages in an environment:

`> conda list -n test_env`

- To add a package to an existing environment:

`> conda install --name <environment_name> -c <chanel_name> <package_name>`

- Get a list of all my environments (Active environment shown with *)

`> conda info -e`

---

## References

- [Ref 1](https://conda.io/en/latest/)
- [Ref 2](https://docs.conda.io/projects/conda/en/latest/user-guide/install/macos.html)
- [Ref 3](https://geohackweek.github.io/Introductory/01-conda-tutorial/)
