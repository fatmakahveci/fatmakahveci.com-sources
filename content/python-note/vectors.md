---
title: Vectors
description: Vectors
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
```python
from math import hypot

class Vector:

  def __init__(self, x=0, y=0):
    self.x = x
    self.y = y

  def __abs__(self):
    return hypot(self.x, self.y)

  # Returns False if the magnitude of the vector is zero.
  # Otherwise, returns True.
  def __bool__(self):
    return(bool(abs(self)))
```

- If `__bool__` is not implemented, Python tries to invoke `x.__len__()`, and if that returns zero, bool returns False. Otherwise, bool returns True.
