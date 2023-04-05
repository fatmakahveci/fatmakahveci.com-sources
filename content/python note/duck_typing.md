---
title: Duck typing
description: Duck typing
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
- When you don't care about the type of object but rather only whether it has certain methods or behaviour.
  - "If it walks like a duck and quacks like a duck, then it's a duck."

```python
# Example: You can verify that an object is iterable if it implemented the iterator protocol.
def isiterable(obj):
  try:
    iter(obj)
    return True
  except TypeError:
    return False
```
