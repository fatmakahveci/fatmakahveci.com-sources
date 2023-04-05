---
title: Memory management
description: Memory management
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
- Data processing and concurrent processing

## Memory allocation

- `Memory allocation` is the assignment of an empty block of space in physical or virtual memory.

### 1. Static memory allocation

- The program is allocated memory at compile time.
- `Stack` is used for implementing static allocation.
  - Here memory cannot be reused.
  - `static int a=10;` # C/C++

- Methods and variables are created in `Stack` memory.
  - A stack frame is created whenever methods and variables are created.
    - These frames are destroyed automatically whenever methods are returned.

### 2. Dynamic memory allocation

- The program is allocated memory at runtime.
- `Heap` is used for implementing dynamic allocation.
  - Here memory can be freed and reused when not required.
  - `int *p; p=new int` # C/C++
- Dynamic memory allocation underlies Python memory management because everything in python is an object.

- Objects and instance variables are created in `Heap` memory.
  - As soon as the variables and functions are returned, dead objects will be garbage collected.

## Python memory manager

- `The raw memory allocator` interacts with the memory manager of the OS to ensure that there's space on the private heap.
  - There's a private `heap` that contains all Python objects and data structures.

- Memory manager manages the heap on demand.
- It has object-specific allocators.
- If the objects get destroyed, it fills this space with a new object of the same size.
- It manages chunks of memory called `blocks`.
  - A collection of `blocks` makes up the `pool`.
    - `Pool`s are created on `Arena`s.
