---
title: Decorator
description: Decorator
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
- A decorator is a function that takes another function as an argument, adds some functionality, and returns another function without altering the source code.
- This is also called metaprogramming because a part of the program tries to modify another part of the program at compile time.
- Decorators can serve to
  - shorten code
  - speed up code
  - change the way that codes acts

## 1. Function decorator

- Function decorators are more common than class decorators.

- If there is more than one decorator for a function, the order of the decorators is important.

```python
def make_pretty(func): # decorator acts as a wrapper
  def inner():
    print("I got decorated")
    func()
  return inner

def ordinary():
  print("I am ordinary")

pretty = make_pretty(ordinary)
pretty() # I got decorated I am ordinary

## 
@make_pretty
def ordinary():
  print("I am ordinary")

# equals to

def ordinary():
  print("I am ordinary")

ordinary = make_pretty(ordinary)
##
```

### Chaining decorators in python

```python
def star(func):
  def inner(*args, **kwargs):
    print("*" * 30)
    func(*args, **kwargs)
    print("*" * 30)

def percent(func):
  # i.e. we don't know the arguments that func will take
  def inner(*args, **kwargs):
    print("%" * 30)
    func(*args, **kwargs)
    print("%" * 30)

@star
@percent
def printer(msg):
  print(msg)

printer("Hello") # printer = star(percent(printer))
```

### Stateful decorators

- We can use a decorator to keep track of the state.

```python
"""
Counts the times for function calling
Output:
  Call 1 of 'say'
  Hello!
  Call 2 of 'say'
  Hello!
  2
"""
from functools import wraps

def count_calls(func):

  @wraps
  def wrapper(*args, **kwargs):
    wrapper.num_calls += 1
    print(f"Call {wrapper.num_calls} of {func.__name__!r}")
    return func(*args, **kwargs)

  wrapper.num_calls = 0
  return wrapper

@count_calls
def say():
  print("Hello!")

say()
say()
print(say.num_calls)
```

## 2. Class decorator

```python

def decorator_function(original_function):
  def wrapper_function(*args, **kwargs):
    print('wrapper executed this before {}'.format(original_function.__name__))
    return original_function(*args, **kwargs)
  return wrapper_function

##

class decorator_class(object):

  def __init__(self, original_function):
    self.original_function = original_function

  def __call__(self, *args, **kwargs):
    print('call method executed this before {}'.format(original_function.__name__))
    return self.original_function(*args, **kwargs)


@decorator_class
def display():
  print('display function ran')


@decorator_class
def display_info(name, age):
  print('display_info ran with arguments ({}, {})'.format(name, age))


display_info('John', 25)

display()
```

---

## classmethod

`<class_method>(cls, <parameter>, <parameter>)`

- `@classmethod` decorator marks a method as a class method.
- It takes the `cls` parameter that points to the class, not the object instance.
- It can't modify the object instance state.
- Class methods are called via the Class containing it, rather than from an instance.
- The `cls` parameter allows `@classmethod` to easily instantiate the class.

```python
class ATM(Bank):
    def __init__(self, balance):
        super().__init__(balance)

class Bank():
  def __init__(self, balance):
    self.balance = balance
  
  @classmethod
  def find_interest_class_method(cls, load_money):
    return loan_money * 1.4

atm = ATM(1000)
Bank.find_interest_classmethod(atm.balance))
```

```python
class Pizza:
    def __init__(self, ingredients):
        self.ingredients = ingredients

    def __repr__(self):
        return f'Pizza({self.ingredients!r})'

    @classmethod
    def margherita(cls):
        return cls(['mozzarella', 'tomatoes'])

    @classmethod
    def prosciutto(cls):
        return cls(['mozzarella', 'tomatoes', 'ham'])

Pizza.margherita() # Pizza(['mozzarella', 'tomatoes'])
```

---

## Examples

```python
# division
"""
It is going to divide 2 and 5
0.4
"""

def smart_divide(func):
    def inner(a, b):
        print(f"It is going to divide {a} and {b}")
        if b == 0:
            print("{b} is equal to 0.")
            return
        return func(a, b)
    return inner

@smart_divide
def divide(a, b):
    print(a/b)

if __name__ == "__main__":
    divide(2,5)
```

```python
# print stars
"""
******************************
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
Hello
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
******************************
"""

def star(func):
    def inner(*args, **kwargs):
        print("*" * 30)
        func(*args, **kwargs)
        print("*" * 30)
    return inner


def percent(func):
    def inner(*args, **kwargs):
        print("%" * 30)
        func(*args, **kwargs)
        print("%" * 30)
    return inner


@star
@percent
def printer(msg):
    print(msg)


printer("Hello")
```

---

## @property

- It is used to customize getters, setters, and deleters for class attributes.

```python
"""
Output:
  Setting value...
  Getting value...
  37
  Getting value...
  98.60000000000001
"""
class Celsius:
    def __init__(self, temperature=0):
        self.temperature = temperature

    def to_fahrenheit(self):
        return (self.temperature * 1.8) + 32

    @property
    def temperature(self):
        print("Getting value...")
        return self._temperature

    @temperature.setter
    def temperature(self, value):
        print("Setting value...")
        if value < -273.15:
            raise ValueError("Temperature below -273 is not possible")
        self._temperature = value

human = Celsius(37)
print(human.temperature)
print(human.to_fahrenheit())
```

---

## register

- Register a function as a handler for an event.
- It allows two or more subsystems to communicate without knowing much about each other, decoupling design.

```python
from atexit import register

@register
def goodbye():
    print('You are now leaving the Python sector.')
```

---

## staticmethod

- It can be called both a class instance and from a class without instantiating the class first.

```python
"""
@staticmethod
def <function_name>():
    ...
"""

class Student():
    def __init__(self, mark):
        self.mark = mark
    
    @staticmethod
    def find_min(mark):
        return min(mark, 100)

print(Student.find_min(20))
```

---

## wrapper

```python
"""
wrapper executed this before display_info
display_info ran with arguments (John, 25)
wrapper executed this before the display
display function ran
"""

def decorator_function(original_function):
  def wrapper_function(*args, **kwargs):
    print(f"wrapper executed this before {original_function.__name__}")
    return original_function(*args, **kwargs)
  return wrapper_function


@decorator_function
def display():
  print('display function ran')


@decorator_function
def display_info(name, age):
  print(f"display_info ran with arguments ({name}, {age})")


display_info('John', 25)

display()
```
