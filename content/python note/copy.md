---
title: Copy
description: Copy
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

## Copy an Object in Python

- `=` does not create a new object. It only creates a new variable that shares the reference of the original object.

```python
old_list = [[1, 2, 3], [4, 5, 6], [7, 8, 'a']]
new_list = old_list

new_list[2][2] = 9

print('Old List:', old_list) # Old List: [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
print('ID of Old List:', id(old_list)) # ID of Old List: 140673303268168

print('New List:', new_list) # [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
print('ID of New List:', id(new_list)) # ID of New List: 140673303268168
```

[Ref](https://www.programiz.com/python-programming/shallow-deep-copy)

## deepcopy

`import copy`

- `copy.deepcopy(<object>)` returns a deep copy of the object.

- The old_list and new_list are independent.

```python
import copy

old_list = [[1, 1, 1], [2, 2, 2], [3, 3, 3]]
new_list = copy.deepcopy(old_list)

old_list[1][0] = 'BB'

print("Old list:", old_list) # Old list: [[1, 1, 1], ['BB', 2, 2], [3, 3, 3]]
print("New list:", new_list) # New list: [[1, 1, 1], [2, 2, 2], [3, 3, 3]]
```

[Ref](https://www.programiz.com/python-programming/shallow-deep-copy)

## shallowcopy

`import copy`

- `copy.copy(<object>)` returns a shallow copy of the object.

- It creates a new object which stores the reference of the original elements.

- It doesn't create a copy of nested objects, instead, it just copies the reference of nested objects.

- The new_list contains references to the original nested objects stored in the old_list. Then we add the new list i.e [4, 4, 4] into the old_list. This new sublist was not copied in the new_list.

```python
import copy

old_list = [[1, 1, 1], [2, 2, 2], [3, 3, 3]]
new_list = copy.copy(old_list)

old_list.append([4, 4, 4])

print("Old list:", old_list) # Old list: [[1, 1, 1], [2, 2, 2], [3, 3, 3], [4, 4, 4]]
print("New list:", new_list) # New list: [[1, 1, 1], [2, 2, 2], [3, 3, 3]]
```

- When you change any nested objects in old_list, the changes appear in new_list.

```python
import copy

old_list = [[1, 1, 1], [2, 2, 2], [3, 3, 3]]
new_list = copy.copy(old_list)

old_list[1][1] = 'AA'

print("Old list:", old_list) # Old list: [[1, 1, 1], [2, 'AA', 2], [3, 3, 3]]
print("New list:", new_list) # New list: [[1, 1, 1], [2, 'AA', 2], [3, 3, 3]]
```

---

[Ref](https://www.programiz.com/python-programming/shallow-deep-copy)
