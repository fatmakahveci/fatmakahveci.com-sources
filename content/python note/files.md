---
title: Files
description: Files
summary: "Files"
date: 16-02-2023
categories:
  - "Coding"
tags:
  - "python"
  - "coding"
  - "algorithms"
  - "data structures"
---

![files.png](files.png)

## File modes

- `r`
- `w`
- `x` write-only mode; creates a new file, but fails if the file path already exists.
- `r+`
- `a`
- `b` add to mode for binary files (i.e., rb, wb)
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
