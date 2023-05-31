---
title: Combinatorial search
description: Combinatorial search
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
## A* heuristic

## Backtracking

- A systematic way to run through all the possible configurations of a search space.
  - Configurations
    - permutations:= all possible arrangements of objects
    - subsets:= all possible ways of building a collection of them
    - enumerating all spanning trees of a graph, all paths between two vertices, or all possible ways to partition vertices into colour classes
- We must generate each possible configuration exactly once.
- At each step in the backtracking algorithm, we try to extend a given partial solution $a = (a_1, a_2, ..., a_k)$ by adding another element at the end. After this extension, we must test whether what we now have is a complete solution: if so, we should print it or count it. If not, we must check whether the partial solution is still potentially extendable to some complete solution.

![pseudo_code](/img/backtracking_pseudo.png)

### Constructing all paths in a graph

### Constructing all permutations

### Constructing all subsets

## Best-first search

## Search pruning

## Sudoku
