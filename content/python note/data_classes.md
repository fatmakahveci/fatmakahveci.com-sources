---
title: Data classes
description: Data classes
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

- dataclasses == python objects
- dataclass is mutable.

```python
from dataclasses import dataclass

@dataclass
class Student:
  name: str
  id: int
  age: int = 10
  year: int = 5
  
  def birthday(self):
    self.age += 1
 
bob = Student("bob", 123)
bob.birthday() # age = 11
print(bob)

print(bob == ("bob", 123, 10, 5)) # False
print(dataclasses.astuple(bob) == ("bob", 123, 10, 5)) # True
```

- dataclass can be made immutable.

```python
from dataclasses import dataclass

@dataclass(frozen=True) # immutability
class Point:
  x: int
  y: int

origin = Point(0, 0)
# origin.x += 1 # it throws an error
origin.__dict__["x"] = 1 # to change the value of immutable
```
