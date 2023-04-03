---
title: OrderedDict
description: OrderedDict
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

- Order is defined by the insertion order of keys.
- `OrderedDict` is mutable.
- Two functions differ from `dict`.

## 1. `move_to_end()`

`move_to_end(<key>,<last>)` # KeyError if `<key>` is not found. # `<last>=True` if to the end, `<last>=False` if to the beginning

- It moves an item to the end or beginning.

## 2. `popitem()`

- It pops efficiently from either end

- You can check the equality of two dicts efficiently with `OrderedDict`.
- `seq` (`list`, `tuple`)'s order is obvious.
- `set`'s order is not known until it is created.

```python
from collections import OrderedDict

###
nums = OrderedDict('one': 1,'two': 2)
nums.update('two':2.0) # preserves the order
reversed(nums)
#
keys= ['one', 'two']
OrderedDict.fromkeys(keys,0) # 'one': 0, 'two': 0
###
```
