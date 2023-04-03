---
title: Callable types
description: Callable types
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

```python
import random

class BingoCage:

  # accepts any iterable
  def __init__(self, items):
    self._items = list(items)
    random.shuffle(self._items)
  
  def pick(self):
    try:
      return self._items.pop()
    except IndexError:
      raise LookupError('pick from empty BingoCage') # raise if self._items is empty
  
  def __call__(self):
    return self.pick() # shortcut to bingo.pick(): bingo()
    
```
