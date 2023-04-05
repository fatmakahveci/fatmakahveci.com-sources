---
title: Stack
description: Stack
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
- LIFO
- i.e. the pile of plates
- Operations
  - **push:** put a new plate on top. O(1)
  - **pop:** remove the top plate. O(1)
  - **peak:** get the value of the top element without removing it.
  - **is_empty**
  - **is_full**

- Applications
  - reverse a word

```python
class Stack:

 def __init__(self):
  self.stack = []

 def is_empty(self):
  return self.stack == []

 def push(self, item):
  self.stack.append(item)

 def pop(self):
  if self.is_empty():
   return -1
  return self.stack.pop()

 def size(self):
  return len(self.stack)

 def peek(self):
  return self.stack[0]

 def __str__(self):
  return " ".join(map(str,self.stack))

stack_ = Stack()
stack_.push(1)
print(stack_)
stack_.pop()
print(stack_)
stack_.push(1)
stack_.push(2)
print(stack_)
```

## Monotonic stack

- A stack of which elements are all monotonic decreasing or increasing.
