---
title: iterator
description: iterator
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

## iterators vs. iterables

### i. iterables

- An object capable of returning its members one at a time is iterable:
  - All sequence types: `list`, `str`, `tuple`, `bytes`, etc.
  - Some non-sequence types: `dict`, `file objects`, etc.
  - Objects of any classes you define with an `__iter__()` method or with a `__getitem__()` method that implements `Sequence` semantics.
    - Sequence is an iterable which:
      - supports efficient element access using integer indices via the `__getitem__()` method.
      - defines a `__len__()` method that returns the length of the sequence.
- An infinite series of numbers cannot be stored in a collection.
- Every collection in Python is iterable.

### ii. iterators

- It produces the next value with `next()`.
- An iterator is an object representing a stream of data.
- Iteration is often implicit.
- It returns the data one element at a time.
- `__next__()` returns the next element of the stream.
- If there are no more elements in the stream, `__next__()` must raise the `StopIteration` exception.
- An iterator doesn't have to be finite.
- An important foundation for writing functional-style programs.
- It raises `TypeError` if the object doesn't support iteration.
- `max()`, `min()`, `in`, and `not in` support iterators. (`max()` and `min()` never end for infinite iterators.)
- Two common operations on an iterator's output:
    1. Performing some operation for every element.
    2. Selecting a subset of elements that meet some condition.

## Iterating over iterables: next()

```python
word = 'Da'
it = iter(word)
next(it) # D
next(it) # a
next(it) # No values to return StopIteration error is thrown
```

## Iterating at once with * (Splat operator)

- This star operator unpacks all elements of an iterator or an iterable.
- Once you do so, you cannot do it again.

```python
word = 'Data'
it = iter(word)
print(*it) # D a t a
```

## Iterating over

### i. for loop

- We can iterate over a list using a for loop.

```python
employees = [ 'Alice', 'Bob' ]
for employee in employees:
    print(employee)
```

- We can iterate over a range object using a for loop

```python
for i in range(4):
    print(i)
```

### ii. dictionaries

```python
pythonistas = {'k1': 'v1', 'k2':'v2'}
for k, v in pythonistas.items():
    print(f"{k}:{v} ")
```

### iii. file connections

```python
file = open('file.txt')
it = iter(file)
print(next(it)) # first line of `file.txt`
print(next(it)) # second line of `file.txt`
```

---

```python
L = [1, 2, 3]
it = iter(L)
it.__next()__ # 1
next(it) # 2
next(it) # 3
next(it) # StopIteration error
###
for i in iter(<object>):
    print(i)
# equal to
for i in <object>:
    print(i)
###
L = [('Italy', 'Rome'), ('France', 'Paris'), ('US', 'Washington DC')]
dict(iter(L)) # {'Italy': 'Rome', 'France': 'Paris', 'US': 'Washington DC'}
###
# Parantheses are different. [] := list, () := iterator
line_list = ['  line 1\n', 'line 2  \n', ...]

# Generator expression -- returns iterator
stripped_iter = (line.strip() for line in line_list)

# List comprehension -- returns list
stripped_list = [line.strip() for line in line_list]###

seq1 = 'abc'
seq2 = (1, 2, 3)

# if an expression is creating a tuple, it must be surrounded by parentheses.
[(x, y) for x in seq1 for y in seq2] # [('a', 1), ('a', 2), ('a', 3), ('b', 1), ('b', 2), ('b', 3), ('c', 1), ('c', 2), ('c', 3)]
###
```
