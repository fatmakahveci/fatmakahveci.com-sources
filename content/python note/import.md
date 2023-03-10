---
title: import
description: import
summary: "Updated by Fatma, Mar 07, 2023."
date: 07-03-2023
categories:
  - "Coding"
tags:
  - "python"
  - "coding"
  - "algorithms"
  - "data structures"
---
- If the named module cannot be found, a `ModuleNotFoundError` is raised.

```python
from <module_name> import <functions_or_variables> as <abbr>, <functions_or_variables> as <abbr>
```

## Packages

### 1. Regular packages

- A regular package is typically implemented as a directory containing an `__init__.py` file.
- When a regular package is imported, this `__init__.py` file is implicitly executed, and the objects it defines are bound to names in the package's namespace.

### 2. Namespace packages

- A namespace package serves only as a container for subpackages.
- It may have no physical representation.
