---
title: args and kwargs
description: args and kwargs
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

- We use `*args` and `**kwargs` as an argument when we do not know in advance the number of arguments that will be passed in the functions.

- We can pass a variable number of arguments to a function using two special symbols:
  - `*args` := non-keyword arguments
  - `**kwargs` := keyword arguments

## `*args`

- It passes a variable number of non-keyworded arguments list and on which operation of the list can be performed.

```python
def greet(*names):
    """This function greets all the persons in the names tuple."""

    for name in names:
        print("Hello", name)

greet("Bob", "Alice") # Hello Bob \n Hello Alice

greet("Bob") # Hello Bob
```

## `**kwargs`

- It passes a variable number of keyword arguments dictionary to function on which operation of a dictionary can be performed.

```python
def intro(**data):
    print("Data type of argument:", type(data))

    for key, value in data.items():
        print("{} is {}".format(key, value))

intro(Firstname="Sita", Lastname="Sharma", Age=22, Phone=1234567890)
intro(Firstname="John", Lastname="Wood", Email="johnwood@nomail.com", Country="Wakanda", Age=25, Phone=9876543210)

# Data type of argument: <class 'dict'>
# Firstname is Sita
# Lastname is Sharma
# Age is 22
# Phone is 1234567890

# Data type of argument: <class 'dict'>
# Firstname is John
# Lastname is Wood
# Email is johnwood@nomail.com
# Country is Wakanda
# Age is 25
# Phone is 9876543210

```

## Using `*args` and `**kwargs` in same line to call a function

- At first, you should write `*args`.

```python
def myFun(*args, **kwargs):
    print("args: ", args)
    print("kwargs: ", kwargs)

myFun('geeks', 'for', 'geeks', first="Geeks", mid="for", last="Geeks")
# args: ('geeks', 'for', 'geeks')
# kwargs {'first': 'Geeks', 'mid': 'for', 'last': 'Geeks'}
```

---

[Ref](https://www.geeksforgeeks.org/args-kwargs-python/)
