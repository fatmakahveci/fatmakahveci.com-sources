---
title: Conventions
description: Conventions
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
```python
# Maximum line length should be 79 characters.

# Use 4 consecutive spaces to indicate indentation.

# Use .startswith() and .endswith() instead of slicing.

###

# It  will assume line continuation if code is contained within
# parantheses, brackets, or braces.
def function(arg_one, arg_two,
             arg_three, arg_four):
    return arg_one

###

# with backslash
from mypkg import example1, \
    example2, example3

###

# If line breaking needs to occur around binary operators,
# it should occur before the operator.
total = (first_variable
         + second_variable
         - third_variable)

###

# 5
def function(default_parameter=5):

###

# If there is more than one operator in a statement, adding a single space
# before and after each operator can look confusing. It is better to only add
# whitespace around the operators with the lowest priority, especially
# when performing mathematical manipulation.

y = x**2 + 5
z = (x+y) * (x-y)

# and operator has the lowest priority
if x>5 and x%2==0:
    print('x is larger than 5 and divisible by 2!')

###

list[3:4]

# Treat the colon as the operator with the lowest priority
list[x+1 : x+2]

# In an extended slice, both colons must be
# surrounded by the same amount of whitespace
list[3:4:5]
list[x+1 : x+2 : x+3]

# The space is omitted if a slice parameter is omitted
list[x+1 : x+2 :]

###

my_list = [1, 2, 3]

###

x = 5
y = 6

# Recommended
print(x, y)

###

def double(x):
    return x * 2

double(3)

###

list[3]

###

tuple = (1,)

###

var1 = 5
var2 = 6
some_long_var = 7

###

if my_bool:
    return '6 is bigger than 5'

###

my_list = []
if not my_list:
    print('List is empty!')

###

if x is not None:
    return 'x exists!'

###

if arg is not None:
    # Do something with arg...

###

if word.startswith('cat'):
    print('The word starts with "cat"')

###

if file_name.endswith('jpg'):
    print('The file is a JPEG')

###
```
