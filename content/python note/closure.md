---
title: Closure
description: Closure
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

- A closure is a function object that has access to variables in its enclosing lexical scope, even when the function is called outside that scope.

```python
def outer():
 msg = "Hey"
 
 def inner():
  print(msg)
 
 return inner() # function call

outer() # Hey
```

```python
def outer():
 msg = "Hey"
 
 def inner():
  print(msg)
 
 return inner # return function as an object

f = outer()
f() # Hey
```

- The returned function still works when the original function was deleted.

```python
del outer
f() # Hey
outer() # ERROR
```

- Closures can avoid the use of global values and provides some form of data hiding.

- It provides an object-oriented solution. When **one** or **a few** methods in a class will be implemented, closures can provide an elegant solution.

```python
def make_multiplier_of(n):

 def multiplier(x):
  return x * n

 return multiplier

times3 = make_multiplier_of(3)
times5 = make_multiplier_of(5)

print(times3(9)) # 27
```
