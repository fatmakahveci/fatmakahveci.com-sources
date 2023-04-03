---
title: inspect
description: inspect
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

- In Python Introspection is the ability of an object to know about its attributes at runtime.
  - A function knows its name and documentation.
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
