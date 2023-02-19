---
title: Walrus
description: Walrus
summary: "Walrus"
date: 16-02-2023
categories:
  - "Coding"
tags:
  - "python"
  - "coding"
  - "algorithms"
  - "data structures"
---

```python

numbers = [ 2, 8, 0, 1, 1, 9, 7, 7 ]
description = { "length": (num_length := len(numbers)),
                "sum": (num_sum := sum(numbers)),
                "mean": num_sum / num_length, 
              } # description {'length': 8, 'sum': 35, 'mean': 4.375}

numbers = [ 2, 8, 0, 1, 1, 9, 7, 7 ]
def slow(num):
    return num
results = [ value for num in numbers if (value := slow(num)) > 0 ]
print(results)
```
