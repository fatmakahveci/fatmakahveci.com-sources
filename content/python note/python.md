---
title: python
description: python
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
- Guido van Rossum is the creator of the Python programming language.
- Every number, string, data structure, function, class, module, and so on exist in the Python interpreter in its own “box,” which is referred to as a Python object.
- Python is a high-level programming language that's implemented in `C`.

## Pythonic

- Generic operations on sequences
- built-in tuple and mapping types
- structure by indentation
- strong typing without variable declarations

## Variables

- A python variable name is a symbolic name that is a reference or pointer to an object.
- Avoid the global variables.

```python
if not hasattr(<func>, <var>):
 <func>.<var> = ...
```

---

## string

### Splitting

```python
<string_var>.splitlines()
<string_var>.split('<character>', 1) # 1 means only split once so it will return a two-item list.
```

### Complacent Comma Placement

- Always end your lines with a comma.

```python
names = [
     'Alice',
     'Bob',
]
```

---

### String literal concatenation

```python
my_str = ( 'This is a super long string constant '
      'spread out across multiple lines. '
      'And look, no backslash characters needed!')
```

---

## Using the python interpreter interactively

- The most straightforward way to start talking to Python is in an interactive Read-Eval-Print Loop (REPL) environment. That simply means starting up the interpreter and typing commands to it directly. The interpreter:

**R**eads the command you enter
**E**valuates and executes the command
**P**rints the output (if any) to the console
**L**oops back and repeats the process

---

## Code visualization

- www.pythontutor.com

## Motivation

- Don't Repeat Yourself! Do One Thing!

## Dictionary

- **currying:** deriving new functions from existing ones by partial argument application. (named after _Haskell Curry_.)
