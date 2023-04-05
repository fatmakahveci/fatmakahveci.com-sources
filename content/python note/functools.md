---
title: functools
description: functools
summary: "Updated by Fatma, Mar 28, 2023."
date: 28-03-2023
categories:
  - "Coding"
tags:
  - "Python"
  - "coding"
comments: true
---
- It is for higher-order functions that work on other functions.
- It provides functions for working with other functions and callable objects to use or extend them without completely rewriting them.

## Classes

### partial

- It takes a function that accepts some arguments and turns it into a function that accepts fewer arguments.

```python
"""
partial(func[, *args][, **keywords])

- It is an original function for particular argument values.
- Objects created by `partial()` have three read-only attributes:
  - `partial.func` returns the name of the parent function along with a hexadecimal address.
  - `partial.args` returns the positional arguments provided in the partial function.
  - `partial.keywords` returns the keyword arguments provided in the partial function.
"""

from functools import partial


def power(a, b):
 return a**b

# partial functions
pow2 = partial(power, b = 2)
pow4 = partial(power, b = 4)
power_of_5 = partial(power, 5)

print(power(2, 3)) # 8
print(pow2(4)) # 16
print(pow4(3)) # 81
print(power_of_5(2)) # 25

print('Function used in partial function pow2 :', pow2.func) # Function used in partial function pow2 : <function power at 0x000001CCBBE8C7B8>
print('Default keywords for pow2 :', pow2.keywords) # Default keywords for pow2 : {‘b’: 2}
print('Default arguments for power_of_5 :', power_of_5.args) # Default arguments for power_of_5 : (5, )

###

def add_numbers(x, y):
  return x + y

# adds 5 to its argument
add_five = partial(add_numbers, 5)

###
```

### partialmethod

```python
"""partialmethod(func, *args, **keywords)
- It is a method definition of an already defined function for specific arguments like partial function.
- It is not callable, only a method descriptor that returns a new partialmethod descriptor.
"""

from functools import partialmethod 
  
class Demo: 
    def __init__(self): 
        self.color = 'black'
    def _color(self, type): 
        self.color = type
  
    set_red = partialmethod(_color, type ='red') 
    set_blue = partialmethod(_color, type ='blue') 
    set_green = partialmethod(_color, type ='green') 
  
  
obj = Demo() 
print(obj.color) # black 
obj.set_blue()
print(obj.color) # blue
```

## Functions

### Wrap

- It is a built-in function under the functools module.
- It delivers extra information from the function `f(argument)` to the wrapper function.

```python
"""It applies update_wrapper() to the decorated function.
"""

from functools import wraps

def decorator(f):
 @wraps(f)
 def decorated(*args, **kwargs):
  """Decorator's docstring"""
  return f(*args, **kwargs)

 print('Documentation of decorated : ', decorated.__doc__)
 return decorated

@decorator
def f(x):
 """f's Docstring"""
 return x

print('f name :', f.__name__) 
print('Documentation of f :', f.__doc__)

# Documentation of decorated : f's Docstring
# f name : f
# Documentation of f : f's Docstring

###

""" To avoid the confusion that might be caused by the wrapper
function, use @functools.wraps decorator in the wrapper function, 
which will preserve information about the original function.

@functools.wrap(<function_name>)
def wrapper(*args, **kwargs):
  <function_name>() ...
"""

from functools import wraps

def my_logger(original_function):
  
  import logging

  logging.basicConfig(filename=f'{original_function.__name__}.log', level=logging.INFO)

  @wraps(original_function)
  def wrapper(*args, **kwargs):
    logging.info(f'Ran with args: {args}, and kwargs: {kwargs}')
    return original_function(*args, **kwargs)

  return wrapper

def my_timer(original_function):

  import time
  
  @wraps(original_function)
  def wrapper(*args, **kwargs):
    start_time = time.time()
    result = original_function(*args, **kwargs)
    run_time = time.time() - start_time
    print(f'{original_function.__name__} ran in: {run_time:.4f} sec')
    return result

  return wrapper

@my_timer
@my_logger
def display_info(name, age):

  import time

  time.sleep(1)
  print(f'display_info ran with arguments ({name}, {age})')

display_info("Hank", 30)

# https://www.youtube.com/watch?v=FsAPt_9Bf3U&ab_channel=CoreySchafer

###
```

### update_wrapper

```python
"""update_wrapper(<wrapper_function_name>, <wrapped_function_name>[, assigned][, updated])
It updates a wrapper function to look like the wrapped function.
"""

from functools import partial, update_wrapper

def power(a, b):
 """ a to the power b """
 return a**b

# partial function
pow2 = partial(power, b = 2)
pow2.__doc__ = """a to the power 2"""
pow2.__name__ = "pow2"

print(f'Before: {pow2.__doc__}, {pow2.__name__}') # a to the power 2, pow2

update_wrapper(pow2, power) 

print(f'After: {pow2.__doc__}, {pow2.__name__}')  # a to the power b, power
```

### total_ordering

```python
"""It provides rich class comparison methods that help in comparing
classes without explicitly defining a function for it.
at least one of the comparison methods must be defined from
__lt__, __le__, __eq__, __neq__, __gt__, __ge__
i.e., object.__lt__(self, other) eq function must also be defined.
"""

from functools import total_ordering

@total_ordering
class Student:
 def __init__(self, cgpa):
  self.cgpa = cgpa

 def __lt__(self, other):
  return self.cgpa < other.cgpa

 def __eq__(self, other):
  return self.cgpa == other.cgpa

bob = Student(8.6)
alice = Student(7.5)

print(bob.__eq__(alice)) # False
```

### singledispatch

```python
"""It transforms a function into a generic function.
It is used for function overloadings. The overloaded
implementations are registered using the register()
attribute.
"""

from functools import singledispatch 

@singledispatch
def fun(s): 
    print(s) 

@fun.register(int) 
def _(s): 
    print(s * 2) 

fun('GeeksforGeeks') # GeeksforGeeks
fun(10) # 20
```

### reduce

```python
"""
reduce(<function>, sequence[, initial]) -> value

It applies a function of two arguments repeatedly on the elements
of a sequence to reduce the sequence to a single value.

i.e. reduce(lambda x, y: x^y, [1, 2, 3, 4])) calculates (((1^2)^3)^4)
"""

from functools import reduce

list1 = [2, 4, 7, 9, 1, 3]
sum_of_list1 = reduce(lambda a, b:a + b, list1) # ((2+4)+7+9+1+3)
print("Sum of list1:", sum_of_list1) # 26

list2 = ["abc", "xyz", "def"]
max_of_list2 = reduce(lambda a, b:a if a>b else b, list2) # ((abc, xyz), def)
print("Max of list2:", max_of_list2) # xyz
```

### lru_cache

```python
"""It is used for saving up to the maxsize most recent calls of
a function. It speeds up consecutive runs of functions and operations
using cache.
"""

from functools import lru_cache 

@lru_cache(maxsize = None) 
def factorial(n):
    return n * factorial(n-1) if n >= 1 else 1

print([factorial(n) for n in range(7)]) 
print(factorial.cache_info())

# [1, 1, 2, 6, 24, 120, 720]
# CacheInfo(hits=5, misses=7, maxsize=None, currsize=7)

"""Recursive functions can benefit from lru_cache. Whenever
we run this function, the first few factorial calculations will be
saved into the cache. As a result, next time we go to call the function
we will only need to calculate the factorials that are after the ones
we used prior. Of course, not all factorial calculations will be saved.
"""
```

### cmp_to_key

```python
""" <function_name>(<iterable_name>, cmp_to_key(<comparison_function>)
It converts a comparison function into a key function.
It must return 1, 0, -1 for different conditions.
"""

from functools import cmp_to_key

def cmp_fun(a, b):
 if a[-1] > b[-1]:
  return 1
 elif a[-1] < b[-1]:
  return -1
 else:
  return 0

list1 = ['Bob', 'Alice', 'Carol']
l = sorted(list1, cmp_to_key(cmp_fun))
print('sorted list:', l) # ['Alice', 'Bob', 'Carol']
```
