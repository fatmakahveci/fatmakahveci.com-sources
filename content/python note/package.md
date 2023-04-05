---
title: package
description: package
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
## `__init__.py`

- It tells Python that the directory is a package.
- `__init__.py` exposes the module functionality to the outside world.
- To make code a package, we add an `__init__.py` and put it and the module in a directory with a package name.
- It acts as the main interface to the package when someone uses `import <package>`.
- It contains code to import specific functions from `api.py` so that `cli.py` and our test files can access package functionality like `tasks.add()` instead of having to do `tasks.api.add()`.
