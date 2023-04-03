---
title: Class
description: Class
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

```python
class Employee:
 
 raise_percent = 1.05 # class variable
 num_emp = 0 # keep the number of employees
 
 def __init__(self, name, last, age, pay):
  self.name = name # instance variable
  self.last = last
  self.age = age
  self.pay = pay
  Employee.num_emp += 1
 
 def fullname(self):
  print(f"{self.name} {self.last}")

 def apply_raise(self):
  self.pay = self.pay * self.raise_percent
  ## or
  # self.pay = self.pay * Employee.raise_percent # !!

 @classmethod
 def set_raise(cls, amount):
  cls.raise_percent = amount
 
 @classmethod
 def from_string(cls, emp_str):
  name, last, age, pay = emp_str.split('-')
  return cls(name, last, int(age), float(pay))

 @staticmethod
 def holiday_print(day):
  if day == 'weekend':
   print('This is an off day')
  else:
   print('This is not an off day')
 
emp_1 = Employee("James", "Hughes", "32", 5000)
emp_2 = Employee("Charlie", "Brown", "22", 3000)

emp_1.apply_raise()
print(emp_1.__dict__) # {'name':'James', ...}

emp_1.experience = 10 # it only adds this instance not the remaining instance of the class

Employee.raise_percent = 1.06 # class uzerinden guncelledigimiz icin diger instancelari da guncellenir

emp_1.raise_percent = 1.07 # bu guncellemiyor aksine emp_1.experienceteki gibi yeni bir sey yaratacak

Employee.set_raise(1.06) # instance uzerinden de yapilabilirdik

emp_1 = Employee.from_string('James-Hughes-32-5000')
emp_1.holiday_print('working day')
```

### Class variable vs. Instance variable

- **Instance variable:** Classtan yaratilan objelerin kendilerine ozgu degiskenleri

- **Class variable:** Classtan yaratilan tum objelerde paylasilan degiskenler

### Class method vs. Static method

- `@classmethod` decorator methods take class instead of an instance as the first argument

## `__new__`

- It is called when a class is instantiated.
- It is similar to `__init__`
- It is a static method.
- Precedence `__new__` > `__init__`

```python
from collections import namedtuple

Node = namedtuple('Node', 'val left right')
Node.__new__.__defaults__ = (Node,) * len(Node._fields)
Node() # Node(val=None, left=None, right=None)
```
