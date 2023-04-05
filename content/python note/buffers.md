---
title: Buffers
description: Buffers
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
## Buffer Protocol

- It provides a way to access the internal data of an object.
  - Internal data is a memory array or buffer.
- Certain objects available in Python wrap access to an underlying memory array or buffer, including
  - `bytes`
  - `bytearray`
  - `array.array`

---

[https://docs.python.org/dev/c-api/buffer.html#bufferobjects](https://docs.python.org/dev/c-api/buffer.html#bufferobjects)

## Data buffer

- A region of physical memory storage used to temporarily store data while it is being moved from one place to another, typically in the computer's memory.
- A buffer may be used when moving data between processes within a computer.
- Buffers can be implemented
  - in a fixed memory location in hardware _or_
  - by using a virtual data buffer in software, pointing at a location in the physical memory.
- In all cases, the data stored in a data buffer are stored on a physical storage medium.
- Each application can allocate and deallocate its buffers from the general memory pool.

---

[Ref](https://en.wikipedia.org/wiki/Data_buffer)
