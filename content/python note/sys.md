---
title: sys
description: sys
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
- `sys` provides access to some variables used or maintained by the interpreter and to functions that interact strongly with the interpreter.

## `sys.argv`

- The list of command line arguments passed to a Python script.
- `argv[0]` is the script name.

## `sys.exit([arg])`

- It is used to exit from the Python script. It raises a `SystemExit` exception signalling an intention to exit the interpreter.
- The optional `arg` can be an integer giving the exit status (default: 0).
  - `sys.exit(0)` exits without errors.
  - `sys.exit(1)` exits because of an error.

## `sys.path`

- It provides a list of strings that specifies the search path for modules.

## `sys.stdin`, `sys.stdout`, `sys.stderr`

- They are standard I/O streams provided by python.

## `sys.platform`

- It specifies the platform on which Python is running.
  - `Linux`, `win32`, etc.

## `sys.version`

- It specifies the version of python you are using.

## `sys.modules`

- It is a dictionary of all the modules that have been imported in this Python instance.
  - **keys:** module names as strings
  - **values:** module objects themselves

```python
sys.modules['<module_name>']
```
