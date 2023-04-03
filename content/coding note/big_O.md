---
title: The efficiency of algorithms
description: The efficiency of algorithms
summary: "Updated by Fatma, Mar 28, 2023."
date: 28-03-2023
categories:
  - "Coding"
tags:
  - "big-oh-notation"
  - "coding"
  - "algorithms"
  - "data structures"
---

## Time complexity

- Multiple variables can be found in your runtime.
  - `O(whp)`
  - i.e. `O(AB)` for A: for B: end: end

- We drop the constants in runtime.
  - `O(2N)` = `O(N)`
- Drop the non-dominant terms.
  - `O(N^2+ N)` = `O(N^2)`
- When there is no established relationship between N and M, so we have to keep both variables in there.
  - `O(M + N)` = `O(M + N)`

![big_o_sorting](/img/big_o_sorting.png)

---

$$
Big\ O
$$

- An upper bound on the runtime.
- The algorithm is at least as fast as the given time.

$$
Big\ Omega\ (\Omega)
$$

- A lower bound on time.
- The algorithm won't be faster than the given time.

$$
Big\ Theta\ (\Theta)
$$

- If the algorithm is both big Omega and big O.

### Description of runtime for an algorithm: Best, worst, and expected cases

- There is no particular relationship between the concepts.
- They describe the big O or (big theta) time for particular inputs or scenarios.
- Upper, lower, and tight bounds for the runtime.

## Space complexity

- The amount of memory required by an algorithm.

## Amortized time complexity

- When an algorithm has a very bad time complexity only once in a while beside the time complexity that happens most of the time.
  - *i.e.* When the array is fulfilled, the cost of insertion is in `O(n)`. Otherwise, the cost is `O(1)`.
- Average time is taken per operation if you do many operations.
- [Ref](https://medium.com/@satorusasozaki/amortized-time-in-the-time-complexity-of-an-algorithm-6dd9a5d38045)

## Log N runtimes

- When you see a problem where the number of elements gets halved each time, that will likely be an `O(log N)` runtime.
  - **Logic:** How many times we can multiply 1 by 2 until we get N?
    - i.e. No. elements = 8 => No. elements 4 => No. elements 2 => No. elements 1 (3 times)

## Recursive runtimes

- When you have a recursive function that makes multiple calls, the runtime will often look like `O(branches ^ depth)`, where branches are the number of times each recursive call branches.

## Big O examples

![big_o_example](/img/big_o_example.png)

---

**Prime numbers:** If n is divisible by a number greater than its square root, then it's divisible by something smaller than that. O(sqrt(n))

---

![O(a:b)](/img/O(a:b).png)

`O(a/b)`

---

More questions in cracking the coding interview book.
