---
title: Variables and Argument Passing
description: Variables and Argument Passing
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

```python
a = [1, 2, 3]
b = a
a.append(4) # b = [1, 2, 3, 4]
```

- When you pass objects as arguments to a function, new local variables are created referencing the original objects without any copying.

```python
def append_element(some_list, element):
  some_list.append(element)

data = [1, 2, 3]

append_element(data, 4) # data = [1, 2, 3, 4]
```

---

- To check if two references refer to the same object, use the `is` keyword.
- Comparing with `is` not the same as the `==` operator.

```python
a = [1, 2, 3]
b = a
a is b # True
c = list(a)
a is c # False
a == c # True
```

---

## Convert num to a bit

```python
"{0:b}".format(15)
```
