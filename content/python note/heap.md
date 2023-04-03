---
title: Heap
description: Heap
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
- Heap is a special tree-based data structure, which is an almost complete tree that satisfies the heap property:
  - **Max heap:** parent >= children
  - **Min heap:** parent <= children

- It maintains data semiordered.

## Application of heaps

### Binary heap

- Binary heap is a complete binary tree with the following properties:
  - **Shape property:** All levels are filled except possibly the last level. The last level has all keys as left as possible so the binary heap makes them suitable to be stored in an array.
  - **Heap property:** A binary heap is either _Min Heap_ or _Max Heap_.
    - `Min Heap`'s root must be the minimum.
    - `Max Heap`'s root must be the maximum.

- A binary heap is typically represented as an array, where:
  - The root element will be at arr[0].
  - arr[(i-1)/2] is the parent.
  - arr[2i+1] is the left child.
  - arr[2i+2] is the right child.

### Insertion

- Add to the most left available replace with its parent, if `parent < new`, until `parent > new`.

### Extraction

- Rightmost children to the root and make the replacements.

### Priority queue

- Priority queue is a data structure that stores priorities (comparable values) and perhaps associated information.
- It is similar to a queue, but here values come out in order by priority.
- It can be implemented using Binary Heap.
  - Binary heaps support the following operations in `O(logn)` time:
    - `insert(Q,x)` inserts `x` into `Q`.
    - `delete(Q)` deletes max(min) from `Q`.
    - `find_minimum(Q)` returns the largest(smallest) in `Q`.
    - `extractmax(Q)`
    - `decreasekey()`

![cost_indel](cost_indel.png)

```python
"""
This priority queue implementation uses heapq internally and
shares the same time and space complexities. The difference is
that PriorityQueue is synchronized and provides locking semantics
to support multiple concurrent producers and consumers.

Output:
  (1, 'eat')
  (2, 'code')
  (3, 'sleep')
"""
from queue import PriorityQueue

q = PriorityQueue()

q.put((2, 'code'))
q.put((1, 'eat'))
q.put((3, 'sleep'))

while not q.empty():
  next_item = q.get()
  print(next_item)
```

## Fibonacci heap

[Ref](https://github.com/danielborowski/fibonacci-heap-python)

### Heapify

- Heapify is the process of converting a binary tree into a Heap data structure.
- We can pop off the max of the heap repeatedly and establish a sorted array.

[Ref](https://www.youtube.com/watch?v=t0Cq6tVNRBA&ab_channel=HackerRank)

```python
# import heapq

# min_heap = []
# heapq.heapify(min_heap)

# heap_with_values = [ 3, 1, 2 ]
# heapq.heapify(heap_with_values)
# heapq.heappush(min_heap, 5)
# print(min_heap[0])
# heapq.heappop(min_heap)
# len(min_heap)

# max_heap = [ 1, 2, 3 ]
# max_heap = [-num for num in max_heap]
# heapq.heapify(max_heap)
# heapq.heappush(max_heap, 5)
# print(max_heap[0])
# heapq.heappop(max_heap)
# len(max_heap)

###

def max_heapify(arr, i):
 n = len(arr)
 max_ = i
 l, r = 2*i+1, 2*i+2

 if l < n and arr[l] > arr[max_]:
  max_ = l
 if r < n and arr[r] > arr[max_]:
  max_ = r

 if max_ != i:
  arr[i], arr[max_] = arr[max_], arr[i]
  max_heapify(arr, max_)

def min_heapify(arr, i):
 n = len(arr)
 min_ = i
 l, r = 2*i+1, 2*i+2

 if l < n and arr[l] < arr[min_]:
  min_ = l
 if r < n and arr[r] < arr[min_]:
  min_ = r

 if min_ != i:
  arr[i], arr[min_] = arr[min_], arr[i]
  min_heapify(arr, min_)

def build_heap(arr):
 for i in range(len(arr)//2, -1, -1):
  # max_heapify(arr, i)
  min_heapify(arr, i)


if __name__ == "__main__":

 arr = [ 1, 3, 5, 4, 6, 13, 10, 9, 8, 15, 17 ]
 build_heap(arr)
 
 for num in arr:
  print(num, end=' ')
 print()
```

## Min Heap

```python
class MinHeap:

 def __init__(self, max_size):

  self.max_size = max_size
  self.min_heap = [0] * (max_size + 1)
  self.heap_size = 0

 def add(self, element):

  self.heap_size += 1

  if self.heap_size > self.max_size:
   print("The maximum size of heap is exceeded!")
   self.heap_size -= 1
   return

  self.min_heap[self.heap_size] = element

  index = self.heap_size
  parent = index // 2
  while self.min_heap[parent] > self.min_heap[index] and index > 1:
   self.min_heap[parent], self.min_heap[index] = self.min_heap[index], self.min_heap[parent]
   index = parent
   parent = index // 2

 def peek(self):
  return self.min_heap[1]

 def pop(self):

  if self.heap_size < 1:
   print('Heap is already empty!')
   return sys.max_size

  remove_element = self.min_heap[1]
  self.min_heap[1] = self.min_heap[self.heap_size]
  self.heap_size -= 1
  index = 1
  while index <= (self.heap_size // 2):

   left, right = 2*index, 2*index+1

   if self.min_heap[index] > self.min_heap[left]:
    self.min_heap[index], self.min_heap[left] = self.min_heap[left], self.min_heap[index]
    index = left

   elif self.min_heap[index] > self.min_heap[right]:
     self.min_heap[index], self.min_heap[right] = self.min_heap[right], self.min_heap[index]
     index = right

   else:
    break

  return remove_element

 def size(self):
  return self.heap_size

 def __str__(self):
  return str(self.min_heap[1 : self.heap_size + 1])


if __name__ == "__main__":

 min_heap = MinHeap(5)
 min_heap.add(3)
 min_heap.add(1)
 min_heap.add(2)
 min_heap.add(4)
 min_heap.add(5)
```

```python
import heapq

minHeap = []
heapq.heapify(minHeap)

heapWithValues = [3, 1, 2]
heapq.heapify(heapWithValues)

maxHeap = [1, 2, 3]
maxHeap = [ -x for x in maxHeap ]
heapq.heapify(maxHeap)

print([ -x for x in maxHeap ])
```
