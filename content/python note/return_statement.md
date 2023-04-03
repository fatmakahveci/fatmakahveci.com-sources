---
title: return statement
description: return statement
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

- With `return`, functions send returns value back to the caller code.
- Types:
  1. **Explicit `return` statement:** It terminates a function execution and sends the return value back to the caller code.
  2. Implicit `return` statement:** If you don't write a `return` statement, it returns `None`.

## Short-circuiting loops

- A `return` statement inside a loop performs some kind of short-circuit.
- It breaks the loop execution and makes the function return immediately.

## Using `return` in generator functions

```python
def gen():
    yield 1
    yield 2
    return 3 # indicates that the generator is done and makes the generator raise a `StopIteration`
```
