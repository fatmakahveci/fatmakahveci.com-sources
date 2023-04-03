---
title: Parallel programming
description: Parallel programming
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
## Types of Execution

### 1. Synchronous parallel processing

### 2. Asynchronous parallel processing

- The processes are completed in the same order in which it was started.
- It is achieved by locking the main program until the respective processes are finished.
- It doesn't involve locking.
- The order can be mixed up.
- It is done more quicker.

## Two main objects to implement parallel execution of a function

### 1. Pool Class

#### i. Synchronous execution

- `Pool.map()` and `Pool.starmap()`
  - `map` can take only one iterable as an argument.
  - `map` is more suitable for simpler operations and faster.

- `Pool.apply()` takes an `args` argument that accepts the parameters passed to the `function-to-be-parallelized` as an argument.

- To parallelize a function, initialize a Pool with n number of processors and pass the function you want to parallelize to one of the Pool parallelization methods.

#### ii. Asynchronous execution

- `Pool.map_async()` and `Pool.starmap_async()`
- `Pool.apply_async()`

### 2. Process Class

## How to parallelize a Pandas DataFrame?

[Reference](https://www.machinelearningplus.com/python/parallel-processing-python/)

```python
##############################################################################
## Author: @fatmakhv
## Date: 19/08/2021
## Aim: Count how many numbers exist within a given range in each row
##############################################################################

import multiprocessing as mp
import numpy as np
from time import time


def howmany_within_range(row, minimum, maximum):

 count = 0

 for n in row:
  if minimum <= n <= maximum:
   count += 1

 return count


if __name__ == "__main__":
 
 # Given 2D-matrix (list of lists)
 np.random.RandomState(100)
 arr = np.random.randint(0, 10, size=[200000, 5])
 data = arr.tolist()

 pool = mp.Pool(int(mp.cpu_count()/2))

 results = [pool.apply(howmany_within_range, args=(row, 4, 8)) for row in data]

 pool.close()

 print(results[:10])
```
