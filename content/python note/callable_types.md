---
title: Callable types
description: Callable types
summary: "Callable types"
date: 16-02-2023
categories:
  - "Coding"
tags:
  - "python"
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
