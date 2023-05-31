---
title: Underscores in Python
description: Underscores in Python
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
## `_<variable>`

- A naming convention
- For internal use (like protected)

## `<variable>_`

- When the most fitting name is already taken by a keyword.

## `__<variable>`

- Triggers name mangling when used for class attributes,
  - `__<variable_name>`
  - `__<method_name>`
- Enforced by the Python interpreter.
- Treat it like private

## `__<variable>__`

- Indicates special methods defined by the Python language.
  - Commonly used for operator overloading
- Avoid this naming scheme for your attributes.
- double underscore:= dunder

## `_`

- It indicates that a variable is temporary or insignificant.

---

[Ref](https://dbader.org/blog/meaning-of-underscores-in-python)

---

## Name mangling

- Python’s private and protected members can be accessed outside the class through name mangling.
