---
title: Unpacking
description: Unpacking
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
```python
data = [ 'ACME', 50, 91.1, (2012, 12, 21) ]
_, shares, price, _ = data

##

l1 = [1, 2, 3, 4]
print(l1) # [1, 2, 3, 4]
print(*l1) # 1 2 3 4

l2 = [20, 21]
[l1, l2] = [[1, 2, 3, 4], [20, 21]]
merged_l = [*l1, *l2] # [1, 2, 3, 4, 20, 21]

##

d1 = {"name": "Jake", "number":402}
d2 = {"last_name: "Sky", "grade":74}

# d1 + d2 # ERROR

d_merged = {**d1, **d2} # {"name": "Jake", "number":402, "last_name": "Sky", "grade":74}

# when it has two common keys, it takes the latest value
d3 = {"name: "Sky", "grade":74}
d_merged_2 = d1 = {"number":402, "name": "Sky", "grade":74}

## 

str_list = [*"hey"] # ["h", "e", "y"]
```
