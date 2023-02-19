---
title: return statement
description: return statement
summary: "return statement"
date: 18-02-2023
categories:
  - "Coding"
tags:
  - "python"
  - "coding"
  - "algorithms"
  - "data structures"
---

- With `return`, functions send return value back to the caller code.
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
    return 3 # indicates that the generator is done and make the generator raise a `StopIteration`
```
