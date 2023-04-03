---
title: Generator
description: Generator
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

- It can be thought of as a resumable function. Whereas normal functions execute and return a single result at a time, generators return a sequence of multiple results lazily, pausing after each one until the next one is requested. To create a generator, use the `yield` keyword instead of `return` in a function.
- A generator is a special class of functions that simplify the task of writing iterators.
- A generator returns an iterator that returns a stream of values.
- Any function containing a `yield` keyword is a generator function.
- On reaching a `yield`, the generator's state of execution is suspended and local variables are preserved so you could later resume the function where it left off.
- When you call a generator function, it doesn't return a single value. It returns a generator object that supports the iterator protocol.

```python
def squares(n=10):
  print(f'Generating squares from 1 to {n ** 2}')
  for i in range(1, n + 1):
    yield i ** 2

gen = squares()
for x in gen:
  print(x, end=' ') # 1 4 9 16 25 36 49 64 81 100

###
def make_counter(x):
  print('entering make_counter')
  while True:
    yield x
    print('incrementing x')
    x = x + 1

counter = make_counter(2)

next(counter)
# entering make_counter
# 2

next(counter)
# incrementing x
# 3
```

## Generator expressions

- A generator expression is like a generator function without the function.
- It is like an anonymous function that yields values.
- It is a way to make a generator.
- A `genexp` saves memory by yielding items one by one using the iterator.
- It returns an iterator.

```python
symbols = '#@%*@#$'
# if `genexp` is the single argument in a function call, no need for duplicated parenthesis.
tuple(ord(symbol) for symbol in symbols)

import array
# array constructor takes two arguments, so the parenthesis of `genexp` are mandatory.
array.array('I', (ord(symbol) for symbol in symbols))

# cartesian product
# it produces one item at a time
colours = ['black', 'white']
sizes = ['S', 'M', 'L']
for tshirt in ('%s %s' % (c, s) for c in colours for s in sizes):
  print(tshirt)
```

- A generator can be annotated by the generic type `Generator[YieldType, SendType, ReturnType]`. For example,

```python
def echo_round() -> Generator[int, float, str]:
    sent = yield 0
    while sent >= 0:
        sent = yield round(sent)
    return 'Done'
```
