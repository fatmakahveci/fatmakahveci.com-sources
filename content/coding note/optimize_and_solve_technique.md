---
title: Optimize and solve technique
description: Optimize and solve technique
summary: "Updated by Fatma, Mar 07, 2023."
date: 07-03-2023
categories:
  - "Coding"
tags:
  - "python"
  - "coding"
  - "algorithms"
  - "data structures"
---

## 1. BUD

### Bottlenecks

- A bottleneck is a part of your algorithm that slow down the overall runtime.
  - You have one-time work that slows down your algorithm.
    - **Sort O(N log N)** Optimize this.
    - Find the elements with a particular property. O (N)
  - You have a chunk of work that's done repeatedly.

### Unnecessary work

- break the loop is the remaining is not required, etc.

### Duplicated work

## 2. DIY - Do it yourself

- Think intiutively on a real example.
- Often a bigger example will be easier.

## 3. Simplify and Generalize

- Simplify or tweak some constraint
- Solve this new simplified version of the problem
- Adapt it for the more complex version

## 4. Base Case and Build

- e.g. find permutations of a string
  - find the previous permutation and put the current character in each location.
  - c -> {ab,ba} => cab acb abc cba bca bac
- Solve it for a base case
  - i.e. n=1
- Try to build up from there.
- Base case and build algorithms often lead to natural recursive algorithms.

## 5. Data Structure Brainstorm

- Linked list?
  - not good at accessing and sorting numbers
- Array?
  - sorting is expensive
- Binary tree?
  - good at ordering
- Heap?
  - good at
    - basic ordering
    - keeping track of max and min

## Best Conceivable Runtime (BCR)

- __We can use the runtimes to get a hint for what we need to reduce.__

- __We shouldn't just think the common runtimes, such as O(N log N). It might be O(N^2 k), etc.__

- There is no better way. i.e.
  - Compute the number of elements in two array
    - O(N+M)
  - Find all pairs within an array
    - O(N^2)

- Difference between

  - the best conceivable runtime

    - thinking about what your algorithm does, you are probably doing something wrong

    and

  - the base case runtime

    - for a specific algorithm
    - mostly useless

---

- __Binary search runtime is O(log N).__
- __We cannot search an array --even a sorted array-- in better than O(log N) time.__ 
- __When we're done in terms of optimizing the runtime, we should think about the space complexity.__
  - If we want to use less additional space, that probably means no additional space.
- __Put everything into a hash table. O(N)__