---
title: os (operating system)
description: os (operating system)
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

- It gets information on
  - local directories
  - files
  - processes
  - environment variables

```python
import os

os.getcwd() # get the current directory
os.chdir() # change the current directory
os.path.join('<dir>', '<file_name>') # concatenate the strings
os.path.join(os.path.expanduser('~'), '<dir>') # expand a pathname that uses ~ to represent the current user’s home directory.
os.path.split('<dir>/<file_name>') # ('<dir>', '<file_name>') split the path and file name
('<short_name'>, '<extension>') = os.path.splitext('<file_name>') # split the file name and its extension

metadata = os.stat('<file_name>') # return an object that contains several different types of metadata about the file

metadata.st_mtime # modification time
metadata.st_size # the size of a file
```
