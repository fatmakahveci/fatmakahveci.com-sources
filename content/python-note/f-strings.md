---
title: f-strings
description: f-strings
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
"""
f-strings:
    Faster than %- and str.format() because they are evaluated at runtime rather than constant values.
"""

name = "Bob"
age = 24

print(f"Hello, {name}. You are {age}.")

###

print(f"{2 * 37}") # 74

###

def to_lowercase(input):
    return input.lower()

name = "Bob"
print(f"{to_lowercase(name)} is funny.") # bob is funny.

###

name = "Bob"
print(f"name.lower() is funny.") # bob is funny.

###

class Comedian:
    def __init__(self, first_name, last_name, age):
        self.first_name = first_name
        self.last_name = last_name
        self.age = age

    def __str__(self):
        return f"{self.first_name} {self.last_name} is {self.age}."

    def __repr__(self):
        return f"{self.first_name} {self.last_name} is {self.age}. Surprise!"

new_comedian = Comedian("Eric", "Idle", "74")

# __str__()
print(f"{new_comedian}") # Eric Idle is 74.

# __repr__(): we put r at the end.
print(f"{new_comedian!r}") # 'Eric Idle is 74. Surprise!'

###

# `f` must be placed in front of each line of a multiline string.
name = "Eric"
profession = "comedian"
affiliation = "Monty Python"
message = (
    f"Hi {name}. "
    f"You are a {profession}. "
    f"You were in {affiliation}."
)
print(message) # 'Hi Eric. You are a comedian. You were in Monty Python.'

###

comedian = {'name': 'Eric Idle', 'age': 74}
print(f"The comedian is {comedian['name']}, aged {comedian['age']}.")

###

# date
import datetime

now = datetime.datetime.now()

print(f'{now:%Y-%m-%d %H:%M}')

###

# float precision
val = 12.3

print(f'{val:.2f}')

###

# width
for x in range(1, 11):
    print(f'{x:02} {x*x:3} {x*x*x:4}')

# output:
# 01   1    1
# 02   4    8
# 03   9   27
# 04  16   64
# 05  25  125
# 06  36  216
# 07  49  343
# 08  64  512
# 09  81  729
# 10 100 1000

###

# justify string

s1 = 'a'
s2 = 'ab'
s3 = 'abc'
s4 = 'abcd'

print(f'{s1:>10}')
print(f'{s2:>10}')
print(f'{s3:>10}')
print(f'{s4:>10}')

# output:
#         a
#        ab
#       abc
#      abcd

###
```
