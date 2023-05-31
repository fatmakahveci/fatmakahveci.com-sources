---
title: Operators
description: Operators
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
## Operator overloading

```python
class Point:
    def __init__(self, x=0, y=0):
        self.x = x
        self.y = y

    def __str__(self):
        return f"({self.x},{self.y})"

    def __add__(self, other):
        x = self.x + other.x
        y = self.y + other.y
        return Point(x, y)

p1 = Point(1, 2)
p2 = Point(2, 3)
print(p1+p2) # (3,5)

# __<operator_abbreviation>__:= add, sub, mul, pow, truediv, floordiv, mod, lshift, rshift, and, or, xor, invert
# ... lt, le, eq, ne, gt, ge
```

## Operator precedence

![operator_precedence.png](/img/operator_precedence.png)

## bitwise xor

```python
a = 5            #0101
b = 3            #0011
result = (a ^ b) #0110
```
