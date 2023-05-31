---
title: Files
description: Files
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
![files.png](files.png)

## File modes

- `r`
- `w`
- `x` write-only mode; creates a new file, but fails if the file path already exists.
- `r+`
- `a`
- `b` add to a mode for binary files (i.e., rb, wb)
- `t` text mode for file (automatically decoding bytes to Unicode)

## Check file existence

```python
def check_file_existence(file_name):
 try:
  file = open(file_name, 'r')
  file.close()
 except FileNotFoundError:
  print(f"{file_name} does not exist.")
```
