---
title: Knapsack
description: Knapsack
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
- For given weights and values of $n$ items, we have to choose sets of weights that can fill up the maximum capacity $w$ in a bag of capacity $W$.
- This set should contain a maximum number of items.
- The expected output is an integer with a count of a maximum number of items.

- Applications
  - Resource allocation

- Approaches
  - Greedy
  - DP
  - Brute force

## 0-1 Knapsack

```python
# O(2^n) as there are redundant subproblems
def knapSack(W, wt, val, n):

    if n == 0 or W == 0:
        return 0
 
    if wt[n-1] > W:
        return knapSack(W, wt, val, n-1)
    
    # pick or don't pick
    return max( knapSack(W - wt[n-1], wt, val, n-1) + val[n-1],
                knapSack(W, wt, val, n-1) )
 
val = [60, 100, 120]
wt = [10, 20, 30]
W = 50
n = len(val)
print(knapSack(W, wt, val, n))
```

### 0-1 Knapsack DP

- You cannot break an item
  - pick OR
  - don't pick

```python
def knapSack(W, w, val):
    num_items = len(val)
    m = {}
    for c in range(W+1):
        m[(0,c)] = 0

    for i in range(1, num_items+1):
        for c in range(W+1):
            if w[i-1] <= c:
                m[(i,c)] = max(m[i-1,c], val[i-1]+m[(i-1,c-w[i-1])])
            else:
                m[(i,c)] = m[(i-1,c)]

    return m[(num_items,W)]

print(knapSack(W=50, w=[10, 20, 30], val=[60, 100, 120]))
```
