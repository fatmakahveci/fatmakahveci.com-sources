---
title: Methods
description: Methods
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
## Instance methods

- The basic no-frills method
- It takes one parameter, `self`.
  - `self` points to an instance of `<Class>` when the method is called.
  - You can freely access attributes and other methods on the same object with `self`.

```python
class Pizza:
    def __init__(self, ingredients):
        self.ingredients = ingredients

    def __repr__(self):
        return f'Pizza({self.ingredients!r})'

Pizza(['cheese', 'tomatoes']) # Pizza(['cheese', 'tomatoes'])
```

## Magic methods

- `def __str__(self):` is a magic method.

```python
def __add__(self, other):
 return self.pay + other.pay

def __len__(self):
 return len(self.name)
```

## Special Methods

```python
from math import hypot

class Vector:

  def __init__(self, x=0, y=0):
    self.x = x
    self.y = y

  def __repr__(self):
    return 'Vector(%r, %r)' % (self.x, self.y)

  def __abs__(self):
    return hypot(self.x, self.y)

  def __bool__(self):
    return(bool(abs(self)))

  def __add__(self, other):
    x = self.x + other.x
    y = self.y + other.y
    return Vector(x, y)
  
  def __mul__(self, scalar):
    return Vector(self.x * scalar, self.y * scalar)
```

- They are called by the Python interpreter.
- If `my_object` is an instance of a user-defined class, then Python calls the `__len__` instance method you implemented.
  - Do not write `my_object.__len__()`
  - Write `len(my_object)`

## Static methods

- It takes neither a `self` nor a `cls` parameter.
- It can neither modify object state nor class state.

```python
import math

class Pizza:
    def __init__(self, radius, ingredients):
        self.radius = radius
        self.ingredients = ingredients

    def __repr__(self):
        return (f'Pizza({self.radius!r}, '
                f'{self.ingredients!r})')

    def area(self):
        return self.circle_area(self.radius)

    @staticmethod
    def circle_area(r):
        return r ** 2 * math.pi

p = Pizza(4, ['mozzarella', 'tomatoes'])
p # Pizza(4, ['mozzarella', 'tomatoes'])
p.area() # 50.26548245743669
Pizza.circle_area(4) # 50.26548245743669
```
