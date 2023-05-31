---
title: Dogpile effect
description: Dogpile effect
summary: "Updated by Fatma, Mar 28, 2023."
date: 28-03-2023
categories:
  - "Coding"
tags:
  - "coding"
  - "algorithms"
  - "data structures"
comments: true
---
- The Dogpile effect occurs when the cache expires and websites are hit by numerous requests at the same time. It is triggered because we allowed more than one request to execute the expensive query.
- Dogpile effect can be prevented using semaphore lock. If the value expired, the first process acquires a lock and starts generating new value. All the subsequent requests check if a lock is acquired and serve stale content. After a new value is generated, a lock is released.
