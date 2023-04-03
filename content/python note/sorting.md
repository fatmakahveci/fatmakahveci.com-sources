---
title: Sorting
description: Sorting
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
- A comparison sort cannot perform better than `O(nlogn)` on average.

## Problems that can be reduced to sorting

### Searching

- Search preprocessing: `O(logn)` after sorting
- `O(1)` with hashing

### Closest pair

- Find the pair of numbers that have the smallest difference between them: `O(n)` scan after sorting

### Element uniqueness

- A special case of the closest-pair problem, where the gap is zero.
- `O(n)` with hashing
  - Build a hash table using chaining, and then compare each of the pairs of items within a bucket. If no bucket contains a duplicate pair, then all the elements must be unique.

### Finding the mode

- Given a set of `n` items, which element occurs the largest number of times in the set?
  - By walking to the left of this point until the first element is not k and then doing the same to the right, we can find this count in `O(logn+c)` time, where `c` is the number of occurrences of `k`.
- `O(n)` with hashing
  - Each bucket should contain a small number of distinct elements but may have many duplicates. We start from the first element in a bucket and count/delete all copies of it, repeating this sweep the expected constant number of passes until the bucket is empty.

### Selection

- What is the `k`th largest item in an array?
  - `O(1)` after sorting

### Convex hulls

- What is the polygon of the smallest perimeter that contains a given set of `n` points in two dimensions?

### Find the intersection

1. **Sort the big set** and binary search of the `m` elements: `O((m+n)logn)`
2. **Sort the small set** and binary search of the `n` elements: `O((n+m)logm)`
3. **Sort both:** We can compare the smallest elements of the two sorted sets, and discard the smaller ones if they are not identical. By repeating this idea recursively on the now smaller sets.

## Sorting a list

### Parameters

1. `reverse`
   - If it is`True`, in descending order.
2. `key` is a function that produces a value to sort the objects.

### list.sort

- It sorts a list in-place, which means without making a copy.
  - Returns `None`

```python
b = ['saw', 'small', 'He', 'foxes', 'six']
b.sort(key=len)
```

### sorted

- It creates a new list and returns it.
- It accepts any iterable object as an argument including
  - immutable sequences
  - generators

```python
fruits = ['grape', 'raspberry', 'apple', 'banana']
sorted(fruits, reverse=True) # ['raspberry', 'grape', 'banana', 'apple']
sorted(fruits, key=len) # ['grape', 'apple', 'banana', 'raspberry']
```

## Sorting algorithms

- In-place merge sort
- Introsort
- Block sort
- Timsort
- Selection sort
- Cubesort
- Shellsort
- Bubble sort
- Exchange sort
- Tree sort
- Cycle sort
- Library sort
- Patience sorting
- Smoothsort
- Strand sort
- Tournament sort
- Cocktail shaker sort
- Comb sort
- Gnome sort
- Odd-even sort

## Bucket sort (Distribution sort)

## Heapsort

- Heapsort uses a binary heap to sort an array in `O(nlogn)`.
  - Quick sort is preferred instead of heapsort.
- It can be thought of as an improved selection sort.

## Insertion sort

```python
def insertion_sort(arr):
    for i in range(1, len(arr)):
        j = i
        while j > 0 and arr[j] < arr[j-1]:
            arr[j], arr[j-1] = arr[j-1], arr[j]
            j -= 1
    return arr

if __name__ == "__main__":
    print(insertion_sort([ 7, 1, 5, 2, 6 ]))

# 7 1 5 2 6
#   i
#   j

# 1 7 5 2 6
#     i
#     j

# 1 5 7 2 6
#     i
#   j

# 1 5 7 2 6
#       i
#       j

# 1 5 2 7 6
#       i
#     j

# 1 2 5 7 6
#       i
#   j

# 1 2 5 7 6
#         i
#         j

# 1 2 5 6 7
```

## Merge sort

- Merging two sorted arrays operates in `O(N)` time and `O(1)` space.

```python
def merge_sort(arr):
 if len(arr) == 1:
  return arr
 mid = len(arr) // 2
 return merge(merge_sort(arr[:mid]), merge_sort(arr[mid:]))

def merge(left_arr, right_arr):
 output = []
 i = j = 0
 while i < len(left_arr) and j < len(right_arr):
  if left_arr[i] < right_arr[j]:
   output.append(left_arr[i])
   i += 1
  else:
   output.append(right_arr[j])
   j += 1
 output.extend(left_arr[i:])
 output.extend(right_arr[j:])

 return output


if __name__ == "__main__":
 print(merge_sort([ 54, 26, 93, 17, 77, 31, 44, 55, 20 ]))
```

## Quick sort

- Divide-and-conquer
- It selects a pivot value, which may be chosen in many ways.
- In-place sorting algorithm
- Cases
  - Average: `O(nlogn)`
  - Worst case: `O(n^2)`

```python
from typing import List

def quick_sort(a_list: List[int]) -> None:

 def quick_sort_helper(a_list: List[int], start: int, end: int) -> None:
  if start < end:
   split_point = partition(a_list, start, end)
   quick_sort_helper(a_list, start, split_point - 1)
   quick_sort_helper(a_list, split_point + 1, end)
 
 quick_sort_helper(a_list, 0, len(a_list)-1)
 return a_list

def partition(a_list: List[int], start: int, end: int) -> int:
 pivot_value = a_list[start]

 left = start + 1
 right = end

 done = False

 while not done:

  while left <= right and a_list[left] <= pivot_value:
   left += 1

  while right >= left and a_list[right] >= pivot_value:
   right -= 1

  if right < left:
   done = True
  else:
   a_list[right], a_list[left] = a_list[left], a_list[right]

 a_list[start], a_list[right] = a_list[right], a_list[start]

 return right


if __name__ == "__main__":
 print(quick_sort([54, 26, 93, 17, 77, 31, 44, 55, 20]))
```

## Selection sort

- `O(n^2)`
- `O(nlogn)` with priority queue implementation

```python
def selectionSort(arr):
  for i in range(len(arr)):
    min = i
    for j in range(i+1, len(arr)):
      if (array[j] < arr[min]):
        min = j
    arr[min], arr[i] =  arr[i], arr[min]
  return arr

print(selectionSort([13, 4, 9, 5, 3, 16, 12]))
```
