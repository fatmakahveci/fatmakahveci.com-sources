---
title: atexit - Exit handlers
description: atexit - Exit handlers
summary: "Updated by Fatma, Mar 07, 2023."
date: 07-03-2023
categories:
  - "Coding"
tags:
  - "python"
  - "coding"
  - "algorithms"
  - "data structures"
---

- It performs cleanup after the interpreter exits.

- It has two functions:

## 1. `register()`

- It takes a function as an argument to be executed when the interpreter exits. Execution takes place on a LIFO.

```python
""" Output: Goodbye
"""
from atexit import register

@register
def goodbye():
  print("Goodbye")
```

## 2. `unregister()`

- After calling `unregister()`, `<function_name>` is guaranteed not to be called when the interpreter shuts down, even if it was registered more than once.

```python
"""Output: No output
"""
from atexit import unregister

names = ['Geeks', 'for', 'Geeks']
  
def hello(name):
  print(name)
  
for name in names:
  atexit.unregister(hello)
```
