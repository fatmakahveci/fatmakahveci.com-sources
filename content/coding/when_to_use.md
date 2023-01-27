---
title: When to use data structures and algorithms
description: When to use data structures and algorithms
summary: "When to use data structures and algorithms"
date: 30-11-2022
categories:
  - "Coding"
tags:
  - "python"
  - "coding"
  - "software"
  - "algorithm"
  - "data structure"
  - "python"
  - "runtime"
---

## Algorithms

---

## Arrays

- .

---

## Backtracking

- Generate all
- Compute all
- The problem has mostly exponential time

- 3 keys of backtracking
  - **choice** := decision space that you can choose from
  - **constraints** := your decisions are constrained somehow
  - **goal** := like filling n slots, etc.

- There are three types of problems in backtracking, where we search for
  1. **Decision problem:** a feasible solution
  2. **Optimization problem:** the best solution
  3. **Enumeration problem:** all feasible solutions

- In backtracking, we use recursion to explore all the possibilities until we get the best result for the problem.

---

## Bitwise algorithms

---

## Clarification questions

- What result should be returned for total amount 0?
- What result should be returned if the list/vector contains a single element/no elements?
- What result should be returned if there is no solution?
- What result should be returned when all elements are negative?
- What result should be returned if the matrix does not contain ones?
- What result should be returned for an empty string/matrix/set/sentence/array/vector?
- How long can the list/set/string/vector/n/array be?
- How many queries can we have?
- Are the indices in the queries valid?
- What is the maximum length of the input?
- What is the largest height?
- Is it possible that the amount cannot be paid with the given coins?
- Is it possible that the sentence cannot be split into words?
- Is it possible that no path to the destination exists?
- Can some elements be zero/negative? How should invalid values be handled?
- Can the hand be empty?
- Can cells contain values other than 0 or 1?
- Can there be walls in the starting or ending positions?
- When there are multiple palindromic substrings of the same length, which should be returned?
- Are we looking for palindromes both odd and even lengths?
- Are the indices in the queries valid?
- Suppose that no palindromic substring of length at least 2 exists. Is a substring of length 1 (i.e. a single character) a valid palindrome?
- Should we consider subsequences that are decreasing? Such as [5, 3, 1].
- Should we consider subsequences that are constant? Such as [1, 1, 1].
- Does the dealer know the values of the cards in the deck and their order?
- How large can a hand/maze/matrix be?
- How should we handle invalid regular expressions? For example, '*' or 'a**'.
- What is there are not enough cards in the deck to build a hand of the requested size?

---

## Comments

- Use comments to explain _why_ the code is doing something.
- If you feel the need to explain _what_ it is doing, it might be time to refactor that piece of code into an approximately-named function.
- Add comment like: "TODO: refactor into helper function."

---

## Complexity

### 1. Time complexity

### 2. Space complexity

---

## Design patterns

---

## Dictionaries

- To locate, insert, and delete a record associated any query with key `q`

### Implementations

1. Hash table
2. Skip list
3. Balanced/unbalanced search tree

---

## Divide-and-conquer algorithms

- They break a problem into subproblems, but these subproblems are not overlapping.

---

## Dynamic Programming (DP)

- It is generally the right method for optimization problems on combinatorial objects that have an inherent left-to-right order among components.
  - Left-to-right objects include
    - character strings
    - rooted trees
    - polygons
    - integer sequences

(1) It asks for the optimum value (minimum or maximum) of something, or the number of ways there are to do something. (Also, it might be for greedy.)

- What is the minimum cost of doing...
- What is the maximum profit from...
- How many ways are there to do...
- What is the longest possible...
- Is it possible to reach a certain point...

(2) In case that the future decision depends on the earlier decisions. Deciding to do something at one step may affect the ability to do something in a later step (Here we cannot use greedy algorithms).

### Top-down vs. Bottom-up

- `Top-down` is typically implemented with recursive function and hash map (memoization). Without memoization, this isn't actually DP.
- `Bottom-up` is implemented with iteration (nested for loops and an array) and starts at the base cases.

### Solving DP (i.e. Longest increasing subsequence)

#### 1. Visualize example to see the underlying pattern

- Diagram out what makes a valid solution.

#### 2. Find an appropriate subproblem

- All increasing subsequences are subsets of original sequence.
- All increasing subsequences have a start and end.
- `LIS[k]` = `LIS` ending at index `k`

#### 3. Find relationships among subproblems

- What subproblems are needed to solve `LIS[k]`?
- How do we use these subproblems to solve `LIS[k]`?
  - `LIS[k] = 1 + max{LIS[0], LIS[1], ..., LIS[k-1]}`

#### 4. Generalize the relationship

- How do we solve subproblem `LIS[k]`?

#### 5. Implement by solving subproblems in order

- What order do we solve these subproblems?
- How do we ensure correct ordering if items are given in random order?

- How do we actually get the sequence?
  - Keep track of previous indices

---

## Edge cases

- Handle and eliminate the edge cases early

---

## Exhaustive search

- They try all possibilities and select the best always produce the optimum result, but usually at a prohibitive cost in terms of time complexity.

---

## Flow algorithms

- They can be used to solve general edge and vertex connectivity problems in graphs.

---

## Graphs

- Questions to ask yourself while using graphs:
  - Directed or undirected?
  - Weighted or unweighted?
  - Sparse or dense edges?
  - Which graph representation?
    - Adjacency lists are the right data structure for most applications of graphs.

    ![graph_representation](graph_representation.png)
  
### Depth First Search (DFS)

- Traverse all vertices in a graph
- Traverse all paths between any two vertices in a graph
- Compute a graph's minimum spanning tree
- Detect and find cycles in a graph
- Check if a graph is bipartite
- Find strongly connected components
- Topologically sort the nodes of a graph
- Find bridges/articulation points
- Find augmenting paths in a flow network
- Generate mazes
- Count connected components
- Determine connectivity

### Breadth First Search (BFS)

- Traverse all vertices in a graph
- Find the shortest path between two vertices in a graph where all edges have equal and positive weights, or on unweighted graphs
- Connected components
- Two-coloring graphs

---

## Greedy

- They have optimal substructure, but not overlapping subproblems.
- They make the best local decision at each step are typically efficient, but usually do not guarantee global optimality.

---

## Hashing

---

## Hashmaps

- While they are very fast, you must work with unique and unordered data.

---

## Heaps

---

## Heapsort

- Time complexity
  - Worst-case = $O(nlogn)$
  - Average-case = $O(nlogn)$
  - Best-case = $O(n)$

- Space complexity = $O(1)$
  - Data in an array can be rearranged into a heap, in place.

---

## Linked lists

- .

---

## Median and selection

- Given a set of $n$ numbers or keys and an integer $k$, find the key greater than or equal to exactly $k$ of the $n$ keys.
- Median finding is a special case of selection problem, which seeks the $k^{th}$ element in the sorted order.

### Selection

- Selection arises in several applications:
  1. Filtering outlying elements
  2. Identifying the most promising candidates
  3. Deciles and related divisions
  4. Order statistics

- Issues:
  - How fast does it have to be?
    - The most elementary median finding is $O(nlogn)$
    - `Quick select` is $O(n)$-expected time based on `quicksort`.
  - What if you only get to see each element once?
  - How fast you can find the node?

---

## Memoization

- Memoization is the top-down technique.
  - It starts by breaking the problem down.
  - It stores the completed calculations so that when you need them again, you can look them up instead of needing to compute them an nth time.
  - `Memoization = Recursion + Cache - Recomputing overlapping subproblems`

---

## Monotonic Stack

- It maintains the maximum and minimum elements in the range and keeps the order of elements in the range.

1. It is a range queries in an array problem.
2. The minima/maxima element or the monotonic order of elements in a range is useful to get answer of every range query.
3. When an element is popped from the monotonic stack, it will never be used again.

- It tells `the next greater element`.

---

## Off-by-one Error

- It occurs when a program uses an improper maximum or minimum value that is one more or one less than the proper value.

---

## Optimization

- Find a solution that maximizes or minimizes an objective function
  - i.e. travelling salesman
- It requires proof that they always return the best possible solution.

---

## Permutation

- Generate
  - all permutations of length $n$
  - random permutations of length $n$
  - next permutation of length $n$

- There are two paradigms to construct permutations:
  1. Ranking/unranking methods, can be applied a much wider class of problems
    a. **Ranking:** What is the position of $p=\{p_1, ..., p_n\}$ in the given generation order?
      - A typical ranking function is recursive.
    b. **Unranking:** Which permutation is in position $m$ of the $n!$ permutation of $n$ items?
      - A typical unranking function finds the number of times $(n−1)!$ goes into $m$ and proceeds recursively.
  2. Incremental change methods, more efficient

---

## Queues

- `FIFO`
- Use when the order matters.
- `enqueue(x,q)` inserts `x` at the back of `q`.
- `deque(q)` returns and removes the front from `q`.
- `BFS` in graphs.

---

## Quicksort

- To implement your quicksort:
  1. Use randomization to eliminate $O(n^2)$ time on nearly sorted data.
  2. Use the median of the first, last, and middle elements to increase the likelihood of partitioning the array into roughly equal pieces.
  3. Leave small subarrays for insertion. Terminating the quicksort recursion and switching to insertion sort makes sense when the subarrays get small, say fewer than 20 elements.
  4. Do the smaller partition first.

---

## Recursion

- When a function is breakable into subproblems.
- The function calls itself until it reaches a base case.

---

## Searching

- Programming time
- Certain items may be accessed more often than the others.
  - Put the most common words to the top.
  - Knowledge of access frequencies is easy to exploit with sequential search.
- Access frequencies might change over time.
  - The best self-organizing scheme is move-tofront; that is, we move the most recently searched-for key from its current position to the front of the list.
- Is the key close by?
  - One-sided binary search is faster when $l<<n$.
- Is my data structure sitting on external memory?
  - Once the number of keys grows too large, binary search loses its status as the best search technique.
  - Much better are data structures such as `B-trees` or `van Emde Boas trees`, which cluster the keys into pages to minimize the number of disk accesses per search.
- Can I guess where the key should be?
  - In interpolation search, we exploit our understanding of the distribution of keys to guess where to look next.

### 1. Sequential search

- We start from the front of our list/array of keys and compare each successive item against the search key `q` until we find a match, or reach the end.

### 2. Binary search

- We start with a sorted array of keys. To search for `q`, we compare it to the middle of key $S_{\frac{n}{2}}$. If `q` is before $S_{\frac{n}{2}}$, it must reside in the top half of our set. If not, it must reside in the bottom half of our set. By repeating this process on the correct half, we find `q` using $|-(logn)-|$ comparisons.

#### 2.1. One-sided binary search

- It finds the target at position $p+l$ using at most $2|-lgl-|$ comparisons, so it is faster than binary search when $l<<n$, yet it can never be much worse.
- It is particularly useful in unbounded search problems, such as in numerical root finding.

---

## Set

- To get unique elements and perform lookups.
- If you are doing set logic, use sets:
  - Difference
  - Intersection
  - Symmetric difference
  - Union

---

## Sliding windows

- Iterable items
- Min, max, longest, largest, shortest, contains
- Everything grouped sequentially

---

## Sorting

- Number of keys to be sorted
  - For small data, say <=100, $O(n^2)$ is also fine.
  - For large data, $O(nlogn)$ is required. (heapsort, quicksort, or mergesort)
  - For extremely large data, think about external memory sorting algorithms that minimize disk or network access.

- Existence of duplicated keys
  - Determine which comes first
  - A stable sorting algorithm preserves the original ordering.
    - Most of the $O(n^2)$ algorithms are stable.
    - Many of the $O(nlogn)$ algorithms are not stable.

- About data
  - Partially sorted
    - Insertion sort perform better than they otherwise would.
  - Distribution of keys
    - If the keys are randomly or uniformly distributed, a bucket or distribution sort makes sense.
  - Keys are long or hard to compare
    - Use relatively short prefix to sort
    - Use radix sort. This always takes time linear in the number of characters in the file, instead of $O(nlgn)$ times the cost of comparing two keys.
  - Very small range of possible keys
    - Initialize an n-element bit vector, turn on the bits corresponding to keys, then scan from left to right and report the positions with true bits.

- Should I worry about disk accesses?
  - External sorting := the data is maintained on an external storage device.
    - The simplest approach loads the data into a B-tree and then does an in-order traversal of the tree to read the keys off in sorted order.

---

## Stacks

- `LIFO` tends to happen in the course of executing recursive algorithms.
- Use when retrieval order doesn't matter, such as when processing batch jobs.
- `push(x,s)` inserts `x` at the top of `s`.
- `pop(s)` returns and removes the top of `s`.

---

## Strings

---

## Trees

### 1. AVL Trees

- For indexing large records in databases
- For searching in large databases

---

## 2. Binary trees

General approach to solve the problems:

1. Find one or more base cases
2. Call the same function on the left subtree
3. Call the same function on the right subtree
4. Join the results

```python
def tree_sum(root):
  if not root:
    return 0
  return root.data + tree_sum(root.left) + tree_sum(root.right)
```

```python
def tree_max(root):
  if not root:
    return float("-inf")
  return max(root.data, tree_max(root.left), tree_max(root.right))
```

```python
def tree_height(root):
  if not root:
    return 0
  return 1 + max(tree_height(root.left), tree_height(root.right))
```

```python
def exist_in_tree(root, val):
  if not root:
    return False
  return root.data == val or exist_in_tree(root.left) or exist_in_tree(root.right)
```

```python
def reverse_tree(root):
  if not root:
    return
  reverse_tree(root.left)
  reverse_tree(root.right)
  root.left, root.right = root.right, root.left
```

---

## 3. Binary search trees

- To quickly check whether an element is present in a set or not.

---

### Question variants

#### i. Fixed length

- Max sum subarray of size k

#### ii. Dynamic variant (as in caterpillar example)

- Smallest sum >= to some value S

#### iii. Dynamic variant with auxiliary data structure

- A hash map, a hash set, an additional array, etc.
- Longest substring with no more than k distinct characters
- String permutations

---

## Trie

- Given the list of strings, find all the words.

---
