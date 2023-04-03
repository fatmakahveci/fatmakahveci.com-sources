---
title: docstrings
description: docstrings
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

- It is a string written as the first line of a function.

- Every function in python comes with a __doc__ attribute that holds this information.

## Popular docstring formats

### 1. Google style

```python
def function(arg_1, arg_2=10):
"""Description of what the function does.

Args:
    arg_1 (str): Description of arg_1 that can break onto the next line if needed.
    arg_2 (int, optional): Write optional when an argument has a default value.

Returns:
    bool: Optional description of the return value.
    Extra lines are not indented.

Raises:
    ValueError: Include any error types that the function intentionally raises.

Notes:
    See https://www.datacamp.com/community/tutorials/docstrings-python for more info.
"""
```
  
### 2. Numpydoc

```python
def function(arg_1, arg_2=10):
    """
    Description of what the function does.

    Parameters
    ----------
    arg_1: expected type of arg_1
        Description of arg_1
    arg_2: int, optional
        Write optional when an argument has a default value.
        Default=42.

    Returns
    -------
    The type of the return value
        Can include a description of the return value.
        Replace "Returns" with "Yields" if this function is a generator.
    """
```

### 3. reStructuredText

### 4. EpyText
