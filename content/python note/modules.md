---
title: Modules
description: Modules
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

- A module is a file containing definitions and implementations of classes, functions that can be used inside another program, and variables.

- Do not use `import *` because it affects readability.

- `dir(<package_name>)` returns the names defined by a module.

## How to make a project installable with `pip`

- One directory with one module and a `setup.py` file is enough to make it installable via `pip`.

- `some_module.py` is the code to be shared.

### Example

- In the `<directory>`, both module and setup.py are located `pip install ./<directory>`

some_module_proj/
|- setup.py
|- some_module.py

`$ >> pip install ./some_module_proj`

`$ >> python`

`>>> from some_module import some_func`
`>>> some_func()`
`>>> exit()`
