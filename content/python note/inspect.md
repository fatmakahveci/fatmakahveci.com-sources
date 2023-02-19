---
title: inspect
description: inspect
summary: "inspect"
date: 18-02-2023
categories:
  - "Coding"
tags:
  - "python"
  - "coding"
  - "algorithms"
  - "data structures"
---

- In Python Introspection is the ability of an object to know about its own attributes at runtime.
  - A function knows its own name and documentation.
    - `print(<function_name>.__name__)`

- It gets information about live objects:
  - modules
  - classes
  - methods
  - functions
  - tracebacks
  - frame objects
  - code objects

- It helps you examine
  - the contents of a class
  - retrieve the source code of a method
  - extract and format the argument list for a function
  - get all the information you need to display the detailed traceback

- Main services provided by this module
  - type checking
  - getting source code
  - inspecting classes and functions
  - examining the interpret stack
