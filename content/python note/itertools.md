---
title: itertools
description: itertools
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
- The module’s functions fall into a few broad classes:

1. Functions that create a new iterator based on an existing iterator.
2. Functions for treating an iterator’s elements as function arguments.
3. Functions for selecting portions of an iterator’s output.
4. A function for grouping an iterator’s output.

## Calling functions on elements

```python
"""itertools.starmap(func, iter)
It assumes that the iterable will return a stream of tuples, and calls func using these tuples as the arguments.
"""

itertools.starmap(os.path.join, [('/bin', 'python'), ('/usr', 'bin', 'java')]) # /bin/python, /usr/bin/java
```

## Creating new iterators

```python
"""itertools.count(start, step) := default start: 0, default step: 1
It returns an infinite stream of evenly spaced values.
"""

itertools.count(10, 5) # 10, 15, 20, 25, 30, 35, 40, 45, 50, 55, ...
```

```python
"""itertools.cycle(iter)
It saves a copy of the contents of a provided iterable and returns a new iterator returns its elements from first to last.
The new iterator will repeat these elements infinitely.
"""

itertools.cycle([1, 2, 3, 4, 5]) # 1, 2, 3, 4, 5, 1, 2, 3, 4, 5, ...
```

```python
"""itertools.repeat(<element>, [n]) default: infinite
"""

itertools.repeat('abc') # a, b, c, a, b, c, ...
```

```python
"""itertools.chain(<iterA>, <iterB>, ...)
It takes an arbitrary number of iterable as input.
It returns all of the iterables' elements until all iterators have been exhausted.
"""

itertools.chain(['a', 'b', 'c'], (1, 2, 3)) # a, b, c, 1, 2, 3
```

```python
# itertools.islice(iter, [start], stop, [step])
# It returns a stream that's a slice of the iterator.
# You can't use negative values for start, stop, or step.

itertools.islice(range(10), 2, 8, 2) # 2, 4, 6
```

```python
""" itertools.tee(iter, [n])  default n := 2
It replicates an iterator. It returns n independent iterators that will all return the contents of the source iterator.
It can consume significant memory for large iterators.
"""

itertools.tee( itertools.count() ) # iterA, iterB := iterA -> 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, ... and iterB -> 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, ...
```

## Combinatoric functions

```python
"""itertools.combinations(iterable, r)
"""

itertools.combinations([1, 2, 3], 2) # (1, 2), (1, 3), (2, 3)
```

```python
"""itertools.permutations(iterable, r=None)
"""

itertools.permutations([1, 2, 3, 4, 5], 2) # (1, 2), (1, 3), (2, 1), (2, 3), (3, 1), (3, 2)
```

## Grouping elements

```python
"""itertools.groupby(iter, key_func=None)
key_func(elem) is a function that can compute a key value for each element returned by the iterable.
"""

city_list = [('Decatur', 'AL'), ('Huntsville', 'AL'), ('Selma', 'AL'), ('Anchorage', 'AK'), ('Nome', 'AK'), ('Flagstaff', 'AZ'), ('Phoenix', 'AZ'), ('Tucson', 'AZ')]

def get_state(city_state):
    return city_state[1]

itertools.groupby(city_list, get_state) # ('AL', iterator-1), ('AK', iterator-2), ('AZ', iterator-3), ...
```

## Selecting elements

```python
"""itertools.filterfalse(predicate, iter)
Opposite of filter()
It returns all elements for which the predicate returns false.
"""

itertools.filterfalse(is_even, itertools.count()) # 1, 3, ...
```

```python
"""itertools.takewhile(predicate, iter)
It returns elements for as long as the predicate returns true.
Once the predicate returns false, the iterator will signal the end of its results.
"""
def less_than_10(x):
    return x < 10

itertools.takewhile(less_than_10, itertools.count()) # 0, 1, 2, 3, 4, 5, 6, 7, 8, 9
itertools.takewhile(is_even, itertools.count()) # 0
```

```python
"""itertools.dropwhile(predicate, iter)
It discards elements while the predicate returns True.
It returns the rest of the iterable results.
"""

itertools.dropwhile(less_than_10, itertools.count()) # 10, 11, ...
itertools.dropwhile(is_even, itertools.count()) # 1, 2, 3,
```

```python
"""itertools.compress(data, selectors)
It takes two iterators and returns only those elements of data for which the corresponding element of selectors is true, stopping whenever either one is exhausted.
"""

itertools.compress([1, 2, 3, 4, 5], [True, True, False, False, True]) # 1, 2, 5
```

[Ref](https://docs.python.org/3/howto/functional.html)
