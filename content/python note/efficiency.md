---
title: Efficiency
description: Efficiency
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

## String concatenation

- Do not use `+` for concatenation.
  - Options:
    - `''.join()`
    - `f-strings`

## Use generators

- Generators allow you to create a function that returns one item at a time rather than all items at once.
  - If you have a large dataset, you don't have to wait for the entire dataset to be accessible.

## Assign a function to a local variable

- Python accesses local variables much more efficiently than global variables.
- Assign functions to local variables then use them.

## Get rid of unwanted loops by using itertools

- It also gets rid of the complexity of the code.
