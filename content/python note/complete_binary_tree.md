---
title: Complete binary tree
description: Complete binary tree
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

- Complete binary tree is a binary tree in which all the levels are filled except possibly the lowest one, which is filled from the left.

## Full (Proper) binary tree

- A full binary tree is a binary tree in which every parent node/internal node has either two or no children.

```python
class Node:

 def __init__(self, data):
  self.data = data
  self.leftChild = None
  self.rightChild = None

def isFullTree(root):

 if root is None:
  return True

 if root.leftChild is None and root.rightChild is None:
  return True

 if root.leftChild is not None and root.rightChild is not None:
  return isFullTree(root.leftChild) and isFullTree(root.rightChild)

 return False

root = Node(1)
root.rightChild = Node(3)
root.leftChild = Node(2)

root.leftChild.leftChild = Node(4)
root.leftChild.rightChild = Node(5)
root.leftChild.rightChild.leftChild = Node(6)
root.leftChild.rightChild.leftChild = Node(7)

if isFullTree(root):
 print('A full tree')
else:
 print('Not a full tree')
```
