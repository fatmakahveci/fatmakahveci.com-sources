---
title: Linked Lists
description: Linked Lists
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
- A sequence of nodes
  - Singly-linked list
    - Each node points to the next node
  - Doubly linked list
    - Each node points to both the next and previous nodes
- Unlike an array, access to a particular index is not with a constant time.
  - If you access the Kth element, you iterate through K elements.
- You can add and remove items from the beginning in constant time.

- Linked lists differ from lists in the way that they store elements in memory.

- Lists perform better than linked lists for searching an element.
  - list: O(1) if you know which element you want to access. Otherwise, O(n).
  - linked list: O(n) because you need to traverse the whole list to find the element.

- While lists use a contiguous memory block to store references to their data, linked lists store references as part of their elements.

- Each element is called a `node`. Every node has two fields:
  - `data` contains the value to be stored in the node.
  - `next` contains a reference to the next node on the list.

- A linked list is a collection of nodes.

- The first node is called the `head`.

- The last node's next is `None`.

- The memory usage of both lists and linked lists is very similar.

- to add an element:
  - `insert()`: at a specific position
  - `append()`: at the end

- to remove an element:
  - `remove()`: from a specific position
  - `pop()`: from the end

## Implementing Your Own Linked List

[Ref](https://realpython.com/linked-lists-python/)

```python
class LinkedList:
 def __init__(self):
  self.head = None

 def reverse(self):
  current = self.head
  prev = None
  while current:
   next = current.next
   current.next = prev
   prev = current
   current = next
  self.head = prev

 def printList(self):
  temp = self.head
  while temp:
   print(temp.data)
   temp = temp.next


class Node:
 def __init__(self, data, next):
  self.data = data
  self.next = None

ll = LinkedList()

firstNode = Node(10)
secondNode = Node(20)
thirdNode = Node(30)
fourthNode = Node(40)

ll.head = firstNode
firstNode.next = secondNode
secondNode.next = thirdNode
thirdNode.next = fourthNode

ll.printList()
```

![list_cost.png](/img/list_cost.png)

- `len` is an `O(1)` because in your RAM, lists are stored as tables (series of contiguous addresses). To know when the table stops the computer needs two things: length and start point. That is why `len()` is an `O(1)`, the computer stores the value, so it just needs to look it up.
