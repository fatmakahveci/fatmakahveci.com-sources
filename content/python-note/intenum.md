---
title: intenum
description: intenum
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
import enum

@enum.unique
class LogLevel(enum.IntEnum):
 ERROR = 1
 DEBUG = 2
 WARNING = 3
 FATAL = 4
 INFO = 5
 CRITIC = enum.auto() # it creates automatic value.


def log(level, message):
 print("{}:{}:{}".format(level.name, level.value, message))


if __name__ == "__main__":

 # for level in LogLevel:
  # print("{}:{}".format(level.name,level.value))

 # print(list(level.value for level in LogLevel))

 log(LogLevel.ERROR, "Bu bir hata mesajidir.")
 log(LogLevel.DEBUG, "Bu bir debug mesajidir.")
 log(LogLevel.WARNING, "Bu bir warning mesajidir.")
```
