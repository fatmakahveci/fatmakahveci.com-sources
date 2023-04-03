---
title: Objects
description: Objects
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

- Functions or methods that change an object inplace should return `None` to make it clear to the caller that the object itself is changed, and no new object was created.

## Object references

- Virtually, each data item is an object of a specific type or class in python.

## Object identity

- A unique identifier is given to each created object.
  - `id(<object>)` returns the object's integer identifier.

```python
# Multiple references to a single object
n = 300
m = n # n -> 300 <- m

# Single reference to a single object
n = 300
m = 400 # n -> 300 & m -> 400

# Ophaned object
n = 300 # n -> 300
n = 200 # n -> 200, 300 # where 300 is the orphaned
```

### Smaller integer values

- For optimization, the interpreter creates objects for the integers in the range [-5, 256] at startup, and then reuses them during program execution. Thus, when you assign separate variables to an integer value in this range, they will reference the same object.

```python
m = 30
n = 30
id(m) # 1405569120
id(n) # 1405569120
```

## Immutable and mutable objects

### 1. Immutable objects

- int
- float
- bool
- string
- bytes
- tuple
- frozenset
- None

### 2. Mutable objects

- list
- dict
- set
- byteArray
- objects
- functions
- almost everything else!

---

## Scalar and numeric objects

### 1. Scalar types

- Single value types
  - None
  - str
  - bytes
  - float
  - bool
  - int

### 2. Numeric types

- int
- float
