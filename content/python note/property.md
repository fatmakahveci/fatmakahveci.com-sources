---
title: Property
description: Property
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
## @property

- A pythonic way for getter and setter

```python
# Using @property decorator
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


# create an object
human = Celsius(37)

print(human.temperature)

print(human.to_fahrenheit())

coldest_thing = Celsius(-300)

# Setting value...
# Getting value...
# 37
# Getting value...
# 98.60000000000001
# Setting value...
# Traceback (most recent call last):
#   File "", line 29, in 
#   File "", line 4, in __init__
#   File "", line 18, in temperature
# ValueError: Temperature below -273 is not possible
```
