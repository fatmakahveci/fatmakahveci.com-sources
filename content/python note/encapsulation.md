---
title: Encapsulation
description: Encapsulation
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


```python
class Computer:
 def __init__(self):
  self.__maxprice = 900

 def sell(self):
  print(f"Selling price: {self.__maxprice}")

 def setMaxPrice(self, price):
  self.__maxprice = price

c = Computer()
c.sell() # 900

c.__maxprice = 1000
c.sell() # 1000

c.setMaxPrice(1000)
c.sell() # 1000
```
