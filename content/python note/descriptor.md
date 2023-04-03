---
title: Descriptor
description: Descriptor
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

- It lets objects customize attribute lookup, storage, and deletion.
- Any object which defines the methods
  - `__get__(self, type=None) -> object`,
  - `__set__(self, obj, value) -> None`,
  - `__delete__(self, obj) -> None`, or
  - `__set_name__(self, owner, name)`.

```python
class Verbose_attribute():
    def __get__(self, obj, type=None) -> object:
        return 42

    def __set__(self, obj, value) -> None:
        raise AttributeError("Cannot change the value")

class Foo():
    # To use the descriptor, it must be stored as a class variable in another class.
    attribute1 = Verbose_attribute() 

my_foo_object = Foo()
print(my_foo_object.attribute1) # finds a descriptor instance, recognized by `__get__` method.
```

is the same:

```python
class Foo():
    @property
    def attribute1(self) -> object:
        return 42

    @attribute1.setter
    def attribute1(self, value) -> None:
        raise AttributeError("Cannot change the value")

my_foo_object = Foo()
print(my_foo_object.attribute1)
```
