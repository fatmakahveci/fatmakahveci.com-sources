---
title: Fibonacci
description: Fibonacci
summary: "Updated by Fatma, Mar 07, 2023."
date: 07-03-2023
categories:
  - "Coding"
tags:
  - "python"
  - "coding"
  - "algorithms"
  - "data structures"
---

```python
def fib(n: int) -> int:
 if n < 2: 
  return n
 return fib(n-1) + fib(n-2)


if __name__ == "__main__":
 print(fib(5))
```

## Fibonacci - Memoization

```python
from typing import Dict

memo: Dict[int, int] = {0: 0, 1: 1}


def fib3(n: int) -> int:

 if n not in memo:
  memo[n] = fib3(n-1) + fib3(n-2)

 return memo[n]


if __name__ == "__main__":

 print(fib3(5))
```
