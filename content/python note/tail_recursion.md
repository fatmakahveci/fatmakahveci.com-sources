---
title: Tail Recursion
description: Tail Recursion
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

- Python doesn't support it because it is built more around the idea of iteration than recursion.

```python
# tail_recursion.py
class Recurse(Exception):
    def __init__(self, *args, **kwargs):
        self.args = args
        self.kwargs = kwargs

def recurse(*args, **kwargs):
    raise Recurse(*args, **kwargs)

def tail_recursive(f):
    def decorated(*args, **kwargs):
        while True:
            try:
                return f(*args, **kwargs)
            except Recurse as r:
                args = r.args
                kwargs = r.kwargs
                continue
    return decorated

###

# factorial.py
from tail_recursion import tail_recursive, recurse

# Normal recursion depth maxes out at 980, this one works indefinitely
@tail_recursive
def factorial(n, accumulator=1):
    if n == 0:
        return accumulator
    recurse(n-1, accumulator=accumulator*n)
```
