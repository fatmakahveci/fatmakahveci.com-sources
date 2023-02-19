---
title: Dog pile effect
description: Dog pile effect
summary: "Dog pile effect"
date: 18-02-2023
categories:
  - "Coding"
tags:
  - "python"
  - "coding"
  - "algorithms"
  - "data structures"
---

## Explain what is Dogpile effect? How can you prevent this effect?

The Dogpile effect occurs when cache expires and websites are hit by numerous requests the same time. It is triggered because we allowed more than one request to execute the expensive query.

Dog pile effect can be prevented using semaphore lock. If value expired, first process acquires a lock and starts generating new value. All the subsequent requests check if lock is acquired and serve stale content. After new value is generated, lock is released.
