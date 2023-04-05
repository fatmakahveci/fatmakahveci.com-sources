---
title: Queue
description: Queue
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
- First-In/First-Out (FIFO)

[Ref](https://realpython.com/linked-lists-python/)

```python
class Queue:
 def __init__(self):
  self.size = 0
  self.queue = []

 def enqueue(self, item):
  self.queue.append(item)

 def is_empty(self):
  return len(self.queue) == 0

 def dequeue(self):
  if not self.is_empty():
   self.queue.pop(0)

 def __str__(self):
  return str(f'Queue: {self.queue}')

if __name__ == "__main__":
 q = Queue()
 q.enqueue(5)
 q.enqueue(1)
 q.enqueue(2)
 q.dequeue()
 print(q)
```

## Built-in queue

```python
from collections import deque

dq = deque([ 1, 2, 3 ])

dq.append(4)

dq.appendleft(6)

dq.pop()

dq.popleft()

dq.index(<item>, <start>, <end>)

dq.insert(<index>, <item>)

dq.count(<item>) # number of occurrences of the item

dq.remove(<item>) # removes the first occurrence

dq.extend(<iterable>)

dq.extendleft(<iterable>)

dq.reverse()

dq.rotate(-<num>) # rotates by <num> to left
# 1, 2, 3, 4, 5, 6, 9, 8, 7  => 9, 8, 7
```

## Circular queue

```python
class CircularQueue:

    #Constructor
    def __init__(self):
        self.queue = list()
        self.head = 0
        self.tail = 0
        self.maxSize = 8

    #Adding elements to the queue
    def enqueue(self,data):
        if self.size() == self.maxSize-1:
            return ("Queue Full!")
        self.queue.append(data)
        self.tail = (self.tail + 1) % self.maxSize
        return True

    #Removing elements from the queue
    def dequeue(self):
        if self.size()==0:
            return ("Queue Empty!") 
        data = self.queue[self.head]
        self.head = (self.head + 1) % self.maxSize
        return data

    #Calculating the size of the queue
    def size(self):
        if self.tail>=self.head:
            return (self.tail-self.head)
        return (self.maxSize - (self.head-self.tail))

q = CircularQueue()
print(q.enqueue(1))
print(q.enqueue(2))
print(q.enqueue(3))
print(q.enqueue(4))
print(q.enqueue(5))
print(q.enqueue(6))
print(q.enqueue(7))
print(q.enqueue(8))
print(q.enqueue(9))
print(q.dequeue())
print(q.dequeue())
print(q.dequeue())
print(q.dequeue())
print(q.dequeue())
print(q.dequeue())
print(q.dequeue())
print(q.dequeue())
print(q.dequeue())
```
