---
title: Recursion
description: Recursion
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

- Recursion isn't a strong Python feature due to the inherent recursion limit.

```python
def sum(items):
  head, *tail = items
  return head + sum(tail) if tail else head
```

- Storing partial results would have done no good for such recursive algorithms as quicksort, backtracking, and DFS because all the recursive calls made in these algorithms have distinct parameter values. It doesn't pay to store something you will use once and never refer to again.
