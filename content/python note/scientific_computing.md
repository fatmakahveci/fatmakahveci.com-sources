---
title: Scientific computing
description: Scientific computing
summary: "Updated by Fatma, Mar 28, 2023."
date: 28-03-2023
categories:
  - "Coding"
tags:
  - "Python"
  - "coding"
  - "algorithms"
  - "data structures"
---
## SciPy

- A collection of packages addressing many standard problem domains in scientific computing.

  - `scipy.integrate`
    - Numerical integration routines and differential equation solvers
  - `scipy.linalg`
    - Linear algebra routines and matrix decompositions extending beyond those provided in `numpy.linalg`
  - `scipy.optimize`
    - Function optimizers (minimizers) and root-finding algorithms
  - `scipy.signal`
    - Signal processing tools
  - `scipy.sparse`
    - Sparse matrices and sparse linear system solvers
  - `scipy.special`
    - Wrapper around SPECFUN, a Fortran library implementing many common mathematical functions, such as the gamma function.
  - `scipy.stats`
    - Standard continuous and discrete probability distributions (density functions, samplers, continuous distribution functions), various statistical tests, and more descriptive statistics.

## scikit-learn

- The premier general-purpose machine learning toolkit for Pythonistas.

### Submodules

#### 1. Classification

- SVM
- Nearest neighbours
- Random forest
- Logistic regression

#### 2. Regression

- Lasso
- Ridge regression

#### 3. Clustering

- k-means
- spectral clustering

#### 4. Dimensionality reductions

- PCA
- feature selection
- matrix factorization

#### 5. Model selection

- Grid search
- cross-validation
- metrics

#### 6. Preprocessing

- feature extraction
- normalization

### `Series`

- A `Series` is a sequence of data values.
- If a `DataFrame` is a table, a `Series` is a list.

```python
pd.Series([30,35,40], index=['2015 Sales', '2016 Sales', '2017 Sales'], name = 'Product A')
```
