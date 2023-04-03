---
title: Trees
description: Trees
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

- A nonlinear hierarchical data structure that consists of nodes connected by edges.
- They allow quicker and easier access to data, as they are nonlinear data structures.

## B-tree

- It generalizes the `Binary Search Tree`, allowing more than two children.

## Balanced binary tree

- **Note:** Be familiar with at least one type of balanced binary tree, whether it's a red/black tree, a splay tree or an AVL tree, and know how it's implemented.

- A.k.a. a height-balanced binary tree
  - the height of the left and right subtree of any node differ by not more than 1.

### AVL tree(Adelson-Velskii and Landis Tree) (Height binary tree)

- A balanced binary search tree
- Each node stores a value called a balanced factor, which is the difference in the height of the left subtree and right subtree.
  - All nodes must have a balance factor of -1, 0, and 1.
    - Balance factor = height(left_subtree) - height(right_subtree)

- **Runtime**
  - Insertion `$O(logn)$`
  - Deletion `$O(logn)$`
  - Search `$O(logn)$`

```python
class TreeNode:
    def __init__(self, key):
        self.right = None
        self.left = None
        self.key = key
        self.height = 1

class AVLTree:
    def insert_node(self, root, key):
        if not root:
            return TreeNode(key)

        if key < root.key:
            root.left = self.insert_node(root.left, key)
        else:
            root.right = self.insert_node(root.right, key)

        root.height = 1 + max(self.get_height(root.left),self.get_height(root.right))

        balance_factor = self.get_balance(root)

        if balance_factor > 1:
            if key >= root.left.key:
                root.left = self.left_rotate(root.left)
            return self.right_rotate(root)

        if balance_factor < -1:
            if key <= root.right.key:
                root.right = self.right_rotate(root.right)
            return self.left_rotate(root)

        return root

    def get_height(self, node):
        if not node:
            return 0
        return node.height

    def get_balance(self, root):
        if not root:
            return 0
        return self.get_height(root.left) - self.get_height(root.right)

    def right_rotate(self, z):
        y = z.left
        tree = y.right

        y.right = z
        z.left = tree

        z.height = 1 + max(self.get_height(z.left), self.get_height(z.right))
        y.height = 1 + max(self.get_height(y.left), self.get_height(y.right))

        return y

    def left_rotate(self, z):
        y = z.right
        tree = y.left

        y.left = z
        z.right = tree

        z.height = 1 + max(self.get_height(z.left), self.get_height(z.right))
        y.height = 1 + max(self.get_height(y.left), self.get_height(y.right))

        return y

    def printHelper(self, currPtr, indent, last):
        import sys

        if currPtr != None:
            sys.stdout.write(indent)
            if last:
                sys.stdout.write("R----")
                indent += "     "
            else:
                sys.stdout.write("L----")
                indent += "|    "
            print(currPtr.key)
            self.printHelper(currPtr.left, indent, False)
            self.printHelper(currPtr.right, indent, True)

    def get_min_value_node(self, root):
        if not root or not root.left:
            return root
        return self.get_min_value_node(root.left)

    def delete_node(self, root, key):
        if not root:
            return root
        elif key < root.key:
            root.left = self.delete_node(root.left, key)
        elif key > root.key:
            root.right = self.delete_node(root.right, key)
        else:
            if not root.left:
                temp = root.right
                root = None
                return temp
            elif not root.right:
                temp = root.left
                root = None
                return temp
            temp = self.get_min_value_node(root.right)
            root.key = temp.key
            root.right = self.delete_node(root.right, temp.key)

        if not root:
            return root

        root.height = 1 + max(self.get_height(root.left),self.get_height(root.right))

        balance_factor = self.get_balance(root)

        if balance_factor > 1:
            if self.get_balance(root.left) < 0:
                root.left = self.left_rotate(root.left)
            return self.right_rotate(root)

        if balance_factor < -1:
            if self.get_balance(root.right) > 0:
                root.right = self.right_rotate(root.right)
            return self.left_rotate(root)

        return root

if __name__ == "__main__":
    tree = AVLTree()
    root = None

    nums = [ 33, 13, 52, 9, 21, 61, 8, 11 ]
    for num in nums:
        root = tree.insert_node(root, num)

    tree.printHelper(root, "", True)

    root = tree.delete_node(root, key=13)
    print("After Deletion: ")
    tree.printHelper(root, "", True)
```

### Red black tree

### Splay tree

## Balanced search tree

- They guarantee the height of the tree is always `O(logn)`.
- It keeps the height small for a sequence of insertions and deletions.

## Binary search tree

```python
class Node:
    def __init__(self, key=None):
        self.left = None
        self.right = None
        self.key = key

def search(root, key):
    if root is None or root.key == key:
        return root

    if root.key < key:
        return search(root.right, key)

    return search(root.left, key)

def insert(root, key):
    if not root:
        return Node(key)
    else:
        if root.key < key:
            root.right = insert(root.right, key)
        elif root.key > key:
            root.left = insert(root.left, key)
        else:
            return root
    return root

def inorder(root):
    if root:
        inorder(root.left)
        print(root.key)
        inorder(root.right)

def min_value_node(root):
    if not root:
        return root
    current = root

    while current.left is not None:
        current = current.left

    return current

def delete(root, key):
    if root is None:
        return root

    if key < root.key:
        root.left = delete(root.left, key)
    elif key > root.key:
        root.right = delete(root.right, key)
    else:
        if root.left is None:
            temp = root.right
            root = None
            return temp
        elif root.right is None:
            temp = root.left
            root = None
            return temp
        temp = min_value_node(root.right)
        root.key = temp.key
        root.right = delete(root.right, temp.key)
    return root


if __name__ == "__main__":
    root = None
    root = insert(root, 50)
    root = insert(root, 30)
    root = insert(root, 10)
    root = insert(root, 20)
    root = insert(root, 40)
    root = insert(root, 70)
    root = insert(root, 60)
    root = insert(root, 80)
     
    print ("Inorder traversal of the given tree")
    inorder(root)
     
    print ("\nDelete 20")
    root = delete(root, 20)
    print ("Inorder traversal of the modified tree")
    inorder(root)
     
    print ("\nDelete 30")
    root = delete(root, 30)
    print ("Inorder traversal of the modified tree")
    inorder(root)
     
    print ("\nDelete 50")
    root = delete(root, 50)
    print ("Inorder traversal of the modified tree")
    inorder(root)
```

## Binary tree

- Each parent node can have at most two children.
- Each node has
  - data
  - address of the left child
  - address of the right child

### Properties

1. The maximum number of nodes at level 'l' of a binary tree is 2^l.

### Types of Binary Tree

#### 1. Full Binary Tree

- Every parent node has two or no children.

#### 2. Perfect Binary Tree

- Every internal node has exactly two child nodes and all the leaf nodes are at the same level.

#### 3. Complete Binary Tree

- Every level must be filled.
- All the leaf elements must lean towards the left.
- The last leaf element might not have the right sibling.

#### 4. Degenerate or Pathological Tree

- A single child either left or right.

#### 5. Skewed Binary Tree

- A pathological tree dominated by the left or right nodes.
  - Left skewed binary tree
  - Right skewed binary tree

#### 6. Balanced Binary Tree

- The difference between the height of the left and right subtree for each node is either 0 or 1.

```python
class Node:

 def __init__(self, item):

  self.left = None
  self.right = None
  self.value = item

 def traversePreorder(self):

  print(str(self.value) +' -> ', end='')

  if self.left:
   self.left.traversePreorder()

  if self.right:
   self.right.traversePreorder()

 def traverseInorder(self):

  if self.left:
   self.left.traverseInorder()

  print(str(self.value) +' -> ', end='')

  if self.right:
   self.right.traverseInorder()

 def traversePostorder(self):

  if self.left:
   self.left.traversePostorder()

  if self.right:
   self.right.traversePostorder()

  print(str(self.value) +' -> ', end='')

if __name__ == "__main__":

 root = Node(1)

 root.left = Node(2)
 root.right = Node(3)

 root.left.left = Node(4)

 print("Preorder traversal:", end="")
 root.traversePreorder()

 print()

 print("Inorder traversal:", end="")
 root.traverseInorder()

 print()

 print("Postorder traversal:", end="")
 root.traversePostorder()
```

## Forest

- A collection of disjoint trees.

## n-ary tree
