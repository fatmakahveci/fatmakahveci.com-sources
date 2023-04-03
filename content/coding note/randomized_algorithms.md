---
title: Randomized Algorithms
description: Randomized Algorithms
summary: "Updated by Fatma, Mar 28, 2023."
date: 28-03-2023
categories:
  - "Coding"
tags:
  - "coding"
  - "algorithms"
  - "data structures"
---

## Random sampling

- This is the idea behind opinion polling, where we sample a small number of people as a proxy for the full population. The result should be representative of the full set.

## Randomized hashing

- The worst-case set of keys that all get hashed to the same bucket.
- Suppose we randomly select our hash function from a large family of good ones as the first step of our algorithm.

## Randomized search

- Randomization can also be used to drive search techniques such as simulated annealing.

## Classification of randomized algorithms

### 1. Las Vegas algorithms

- Guarantee correctness
- Usually (but not always) efficient
- i.e. Quicksort

### 2. Monte Carlo algorithms

- Provably efficient
- Usually (but not always correct)
