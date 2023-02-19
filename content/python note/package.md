---
title: package
description: package
summary: "package"
date: 30-11-2022
categories:
  - "Coding"
tags:
  - "python"
  - "coding"
  - "algorithms"
  - "data structures"
---
- `__init__.py` exposes the module functionality to the outside world.
- To make code a package, we add an `__init__.py` and put it and the module in a directory with a package name.

## `__init__.py`

- It tells Python that the directory is a package.

- It acts as the main interface to the package when someone uses `import <package>`.

- It contains code to import specific functions from api.py so that cli.py and our test files can access package functionality like tasks.add() instead of having to do tasks.api.add().
