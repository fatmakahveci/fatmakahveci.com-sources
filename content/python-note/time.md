---
title: time
description: time
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
import os

metadata = os.stat('<file_name>') # return an object that contains several different types of metadata about the file

metadata.st_mtime # modification time

time.localtime(metadata.st_mtime) # time.localtime() converts a time value from seconds-since-the-Epoch # time.struct_time(tm_year=2009, tm_mon=7, tm_mday=13, tm_hour=17, tm_min=25, tm_sec=44, tm_wday=0, tm_yday=194, tm_isdst=1)

ts = time.time()
te = time.time()
time.sleep(1) # 1 sec
```
