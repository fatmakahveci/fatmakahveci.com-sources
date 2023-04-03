---
title: Functions
description: Functions
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

`def <function_name>(<function_name_without_parantheses>):`

- Functions are first-class objects, which means that
  - functions are objects - they can be referenced to, passed to a variable, and returned from other functions as well.
  - functions can be defined inside another function - an inner function - and can also be passed as an argument to another function.
    - Inner functions only exist inside the parent() function as local variables.

```python
"""<another_function_name> = <function_name>()
function() := function
function := object
"""
def inc(x):
  return x + 1

def dec(x):
  return x - 1

def operate(func, x):
  result = func(x)
  return result
```

```python
"""Inner function
"""

def parent():
  print("Printing from the parent() function")
  
  def first_child():
    print("Printing from the first_child() function")

  def second_child():
    print("Printing from the second_child() function")

  second_child()
  first_child()

parent()
```

- When you call a regular function, it gets a private namespace where its local variables are created. When the function reaches a return statement, the local variables are destroyed and the value is returned to the caller. A later call to the same function creates a new private namespace and a fresh set of local variables.

## First-class object

- It is a program entity that can be
  - created at runtime
  - assigned to a variable or element in a data structure
  - passed as an argument to a function
  - returned as the result of a function.
