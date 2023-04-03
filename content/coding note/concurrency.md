---
title: Concurrency
description: Concurrency
summary: "Updated by Fatma, Mar 28, 2023."
date: 28-03-2023
categories:
  - "Coding"
tags:
  - "concurrency"
  - "coding"
  - "algorithms"
  - "data structures"
---

- Concurrency is the ability to handle multiple tasks simultaneously to improve performance and responsiveness.
- Concurrency examples:
  - Web servers handle requests for millions of clients at once.
  - Tablet and phone apps render animations in the UI while simultaneously performing computation and network requests in the background.
  - It hides the latency of I/O operations.
  - It exploits a modern computer’s many processors.
- Simultaneous things in python, like different trains of thought:
  - thread
  - task
  - process

- The state of each one is saved so it can be restarted right where it was interrupted.
- You can only use the keywords `await`, `async with` and `async` for inside asynchronous code.
- Asynchronous code must be contained inside an `async def` declaration, but the declaration can go anywhere `def` is allowed.
- It's not about using multiple cores, it's about using a single core more efficiently.

## Parallelism

- There are multiple concurrent tasks, which also execute at the same time.
- Parallelism implies concurrency, but concurrency doesn't imply parallelism.

## Multitasking

### 1. Preemptive

- Preempting is the OS's switching between works.
- OS can initiate context switch.
- Interrupts applications and gives control.
- Scheduled by OS.
  - time-slicing
  - P1 -
  - P2 -
- It can use all cores.
- It is less resource intensive than the cooperative.
- Preemptive multitasking can be implemented in two ways:
  1. Multiprocessing
  2. Multithreading

### 2. Cooperative

- OS cannot initiate context switch.
- Scheduler never interrupts a running process to another.
- Scheduled by the process.
- It can use only one core.

- P1 - P2 - P1 -

## Bounded processes

- x-bound refers to the limiting factor that prevents that operation from running faster.
- Progress of the process is limited...

### 1. CPU-bound

- by the speed of the CPU.
- CPU-bound operations are typically computations and processing code.
  - i.e. small calculations.

### 2. I/O-bound

- by the speed of the I/O subsystem.
- I/O-bound operations are mostly waiting on a network or other I/O device.
  - i.e. counting the number of lines in a file.
  - i.e. making requests to a web server.
- At the system level, I/O operations can be completed concurrently.
- In Python, because of the GIL, the best we can do is the concurrency of our I/O operations, and only one piece of Python code is executing at a given time.

### 3. Memory-bound

- by the amount of available memory or the speed of memory access.
- i.e. multiplying large matrices.

### 4. Cache-bound

- by the amount and speed of the available cache.

## CPython

- When we say CPython is not thread-safe, we mean that if two or more threads modify a shared variable, that variable may end in an unexpected state.

## Deadlock

- Common problem in
  - Multiprocessing systems
  - Parallel computing
  - Distributed systems

- Deadlock occurs when Coffman conditions hold:
  1. **Mutual exclusion:** Only one process can use the resource at any given instant of time.
  2. **Hold and wait (Resource holding):** A process is holding at least one resource and requests an additional one.
  3. **No preemption:** A resource can be released only by holding process.
  4. **Circular wait:** P1 -> R1 -> P2 -> R2 -> P1 -> ...

## Event Loop

- An event loop is similar to a while True loop that monitors coroutines, taking feedback on what’s idle, and looking around for things that can be executed in the meantime. It can wake up an idle coroutine when whatever that coroutine is waiting on becomes available.
- It loops forever, looking for tasks with CPU-bound work to run while also pausing tasks that are waiting for I/O.

## Global Interpreter Lock (GIL)

- A mutex that protects access to python objects, preventing multiple threads from executing Python bytecodes at once.
- It prevents race conditions and ensures thread safety.
- A Python process can have only one thread running Python code at a time, even if we have multiple threads on a machine with multiple cores.
  - Multiprocessing can run multiple bytecode instructions concurrently because each Python process has its own GIL.
- GIL is released when I/O operations happen.

### Reference counting

- GIL exists because of the memory management way in CPython. In CPython, memory is managed primarily by a process known as reference counting. Reference counting works by keeping track of who currently needs access to a particular Python object, such as an integer, dictionary, or list. A reference count is an integer keeping track of how many places reference that particular object. When someone no longer needs that referenced object, the reference count is decremented, and when someone else needs it, it is incremented. When the reference count reaches zero, no one is referencing the object, and it can be deleted from memory.

## Multithreading

- A multithreaded application running on a multiple-core machine is both concurrent and parallel.
- Multithreading is only useful for I/O-bound work because we are limited by the GIL.

## Multiprocessing

- In multiprocessing, a parent process creates one or more child processes that it manages. It can distribute work to the child process.
- If multiple cores are available, multiprocessing is useful for CPU-intensive tasks.

## Process vs Thread

- Processes and threads are the basic units of concurrency at the OS level.
- In threading, concurrency is achieved using multiple threads, but due to the GIL only one thread can be running at a time.
- In multiprocessing, the original process is forked process into multiple child processes bypassing the GIL.

### 1. Process

- A process is an instance of a program.
- OS creates it to run programs.
- It can have multiple threads.
- Two processes can execute code simultaneously in the same python program.
- It has more overhead than a thread as opening and closing processes take more time.
- Sharing information between processes is slower than sharing between threads as processes do not share memory space.
- It has a memory space that other applications cannot access.
- It can be used for both I/O and CPU-bound workloads.

### 2. Thread

- Threads are spawned by a process, like mini-processes that live inside a process.
  - They share the memory of the process that created them.
- A thread can efficiently read and write to the same variables.
- Two threads cannot execute code simultaneously in the same python program.
- A process always has at least one thread, which is usually known as the `main thread`.

## Race condition

- Race conditions can arise when two threads need to reference a Python object at the same time.
- A flaw that occurs in the timing or the ordering of events that leads to erroneous program behaviour.

## Socket

- A low-level abstraction for sending and receiving data over a network.
- A socket is like a mailbox.
- Sockets support two main operations:
  1. Sending bytes
  2. Receiving bytes
- We write bytes to a socket, which will then get sent to a remote address, typically some type of server. Once we’ve sent those bytes, we wait for the server to write its response back to our socket. Once these bytes have been sent back to our socket, we can then read the result.
