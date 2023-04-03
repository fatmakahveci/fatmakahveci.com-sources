---
title: Thread
description: Thread
summary: "Updated by Fatma, Mar 28, 2023."
date: 28-03-2023
categories:
  - "Coding"
tags:
  - "coding"
  - "algorithms"
  - "data structures"
---

- A thread is alive if its run method is executing.
- OS knows about each thread, and it can interrupt a thread at any time to start running a different thread.
- It is created at the OS level and more expensive to create than coroutines.
- It has a context-switching cost at the OS level. Saving and restoring thread state when a context switch happens eats up some of the performance gains obtained by using threads.
- Each thread has an `Event Loop` object.
