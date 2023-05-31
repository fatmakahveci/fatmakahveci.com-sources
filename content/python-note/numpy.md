---
title: NumPy
description: NumPy
summary: "Updated by Fatma, Mar 28, 2023."
date: 28-03-2023
categories:
  - "Coding"
tags:
  - "Python"
  - "NumPy"
  - "coding"
  - "algorithms"
  - "data structures"
comments: true
---
## numpy - **num**erical **py**thon

- NumPy provides a computational foundation for general numeric data processing.
- The _lingua franca_ for data exchange.
- Functions for performing element-wise computations with arrays or mathematical operations between arrays
- A fast and efficient multidimensional array object `ndarray`
- Tools for reading and writing array-based datasets to disk and working with memory-mapped files
- Linear algebra operations, Fourier transform, and random number generation
- A C API for connecting NumPy with libraries written in C, C++, or FORTRAN.

### Install

```bash
pip install numpy
```

### Import

```python
import numpy as np
```

### Operations

- Fast vectorized array operations for data munging and cleaning, subsetting and filtering, transformation, and any other kinds of computations
- Common array algorithms
  - sorting
  - unique
  - set operations, etc.
- Efficient descriptive statistics and aggregating/summarizing data
- Data alignment and relational data manipulations for merging and joining together heterogeneous datasets
- Expressing conditional logic as array expressions instead of loops with if-elif-else branches

- Group-wise data manipulations
  - aggregation
  - transformation
  - function application

### Efficiency

- NumPy internally stores data in a contiguous block of memory.
- It performs complex computations on entire arrays without the need for `for` loops.

- **NumPy arrays are more efficient for storing and manipulating data than the other built-in Python data structures.**

## Hello world

```python
import numpy as np

# numpy arrays := vectors (1D) and matrices (2D)

my_list = [1, 2, 3]
np.array(my_list)

my_matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
np.array(my_matrix)

np.arange(0, 10) # ([0, 1, ..., 9])
np.arange(0, 11, 2) # ([0, 2, 4, 6, 8, 10])

# np.ones() similar to the zeros
np.zeros(3) # ([0., 0., 0.])
np.zeros((5, 5)) # ([[0., 0., 0., 0., 0.], [0., 0., 0., 0., 0.], [0., 0., 0., 0., 0.], [0., 0., 0., 0., 0.], [0., 0., 0., 0., 0.]])

np.linspace(0, 10, 3) # ([0., 5., 10.]) # 0 and 10 are included.

np.eye(4) # [4x4] identity matrix

# rand creates an array of the given shape and populates it with random samples from a uniform distribution over [0, 1].
np.random.rand(2) # ([0.23565463, 0.46336045])
np.random.rand(5,5) # similar to the previous, but the size is [5x5].

np.random.randn(2) # rand was uniform distribution, this is standard

np.random.randint(1, 100) # low, high # 62
np.random.randint(1, 100, 10) # (low, high, #items) # ([80, 38, 51, 16, 90, 85, 53, 60, 18, 57])

arr = np.arange(25) # ([ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24])
arr.reshape(5, 5) # ([0, 1, 2, 3, 4] , [...], ..., [..., 24])
arr.max()
arr.argmax()
arr.min()
arr.argmin()
arr.shape # (#rows, #cols)
arr.dtype
arr[0]
arr[1:5]
arr[0:5] = 100 # the first five elements are 100
slice_arr = arr[0:6] # slice_arr = ([0, 1, 2, 3, 4, 5])
arr_copy = arr.copy() # to create a copy
arr[0] # the first row
arr[0][1] # arr[row][col]
arr[0, 1] # arr[row, col]

arr = np.arange(1,11)
arr[arr>2] # array([ 3,  4,  5,  6,  7,  8,  9, 10])
```

## Arithmetic operations

```python
arr = np.array([[1., 2., 3.], [4., 5., 6.]])

arr * arr # multiples one-by-one
arr - arr # zero matrix
1 / arr
arr ** 0.5

arr2 = np.array([[0., 4., 1.], [7., 2., 12.]])

arr > arr2 # compares each element one-by-one and returns a boolean matrix
```

## Array creation

### np.arange()

- Return evenly spaced values within a given interval.

```python
# np.arange(<length>)
np.arange(3) # array([0, 1, 2])
np.arange(3.) # array([0., 1., 2.])

# np.arange(start=<start>, stop=<stop> step=<step>)
np.arange(3, 7) # array([3, 4, 5, 6])
np.arange(3, 7, 2) # array([3 5])
```

### array

```python
data = [[1, 2, 3, 4], [5, 6, 7, 8]]
arr = np.array(data)

arr.ndim # 2
arr.shape # (2, 4)
arr.dtype # int64
```

### asarray

### empty_like

### empty

- Creates an array without initializing its values to any particular value.
- It is not safe to assume that `np.empty` will return an array of all zeros.

```python
# creates two nxm matrix in a single one
np.empty((2, 3, 2))
```

### eye

### full_like

### full

### identity

### ones_like

### ones

### zeros_like

### zeros

- `shape` := int or tuple of ints
- `dtype` := data type
- `order` := {'C', 'F'} row-major or col-major order in memory
- `like`:= array_like

- Return: `out`:= ndarray

```python
# np.zeros(<m>)
np.zeros(5) # [0., 0., 0., 0., 0.]
np.zeros((5,), dtype=int) # [0, 0, 0, 0, 0]

# np.zeros((<n>, <m>)) # nxm matrix
np.zeros((2,1))
```

## Assignment

- The “bare” slice [:] will assign to all values in an array.

```python
arr[:] = <value> # it assigns value to each element in matrix
```

## np.column_stack()

- It stacks two 1D-array on top of each other.

## np.diag()

```python
np.diag([1, 2, 3])
```

## File operations

```python
import numpy as np

# load floating numbers from a file
floats = numpy.loadtxt('<file_name>')

# save the variable to the file
numpy.save('<file_name>', <variable>)
```

## floor_divide

- `numpy.floor_divide(<array_like_numerator>, <array_like_denominator>)`

[Ref](https://numpy.org/doc/stable/reference/generated/numpy.floor_divide.html)

## Indexing and slicing

- `arr[i:j]`
- `arr[i][j] <=> arr[i, j]`
- `arr[i]`
  - `arr[i, j, k]`

- The ellipsis `...` is a Python parser.
  - `x[i, ...] <==> x[i, :, :, :,]`

### Boolean indexing

## Matrix

- `data` := array_like or string
- `dtype`:= data
- `copy`:= bool

```python
arr = np.matrix('1 2; 3 4')
# equals to
arr = np.matrix([1, 2], [3, 4])
```

[Ref](https://numpy.org/doc/stable/reference/generated/numpy.matrix.html)

## ndarray

- N-dimensional array similar to `list`, but it has a fixed size and common data type for all elements.
- It is a fast and flexible container for large datasets in Python.
- Items in `ndarray` can be fetched using
  - `a[i, j]` _or_
  - `a[m:n, k:l]` # a 2D slice
- `data.shape` (n, m)
- `data.dtype` _i.e._ `dtype('float64')`

## np.random.randint()

```python
np.random.randint(low=<min_value>, high=<max_value> size=(<n>, <m>))
```

## random.randn()

- Returns a sample(s) from the "standard normal distribution"

```python
from numpy.random import randn

data = {i : randn() for i in range(7)} # [<#>, <#>, <#>, <#>, <#>, <#>, <#>]

data = randn(2, 3) # array([[<#>, <#>, <#>], [<#>, <#>, <#>]])
```

## numpy.random.seed()

- We set seeds to ensure we see the same random numbers each time we run the program.
- `numpy.random.seed()` creates a random number which is generated with a predictable algorithm.

## reshape()

```python
${array_variable}.reshape(${number_of_rows}, ${number_of_columns})
```

## shape

```python
${array_variable}.shape
```

## size

```python
np.size(${array_variable})
```

## T (transpose)

```python
<np_array>.T
```
