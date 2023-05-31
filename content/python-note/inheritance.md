---
title: Inheritance
description: Inheritance
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
class Bird:

 def __init__(self):
  print("Bird is ready")

 def whoisThis(self):
  print("Bird")

 def swim(self):
  print("Swim faster")

class Penguin(Bird):

 def __init__(self):
  super().__init__()
  print("Penguin is ready")

 def whoisThis(self):
  print("Penguin")

 def run(self):
  print("Run faster")


peggy = Penguin() # Bird is ready # Penguin is ready
peggy.whoisThis() # Penguin
peggy.swim() # Swim faster
peggy.run() # Run faster
```

- Childin parenta erisimi var. Ancak once kendisine ait olani kullaniyor.
- **Superclass/Parent Class:** Inherit ettigimiz class. *i.e.* Employee
- **Subclass/Child Class:** Inherit edilen class. *i.e.* IT

- `super()` has two major use cases:
  - to avoid using the base class name explicitly
  - working with multiple inheritance

```python
"""The syntax for a derived class definition
class <DerivedClassName>(<BaseClassName>):
  <statement>
  ...
"""
```

```python
class Employee:
  
  raise_percent = 1.05 # class variable
  num_emp = 0 # kac calisan oldugu bilgisini tutmak icin
  
  def __init__(self, name, last, age, pay):
    self.name = name # instance variable
    self.last = last
    self.age = age
    self.pay = pay
    Employee.num_emp += 1
    
  def apply_raise(self):
    self.pay = self.pay * self.raise_percent

class IT(Employee): # class <subclass>(<superclass>)
  raise_percent = 1.2
  
  def __init__(self, name, last, age, pay, lang):
    super().__init__(name, last, age, pay)
    self.lang = lang

emp_1 = Employee("James", "Hughes", "32", 5000)
emp_2 = Employee("Charlie", "Brown", "22", 3000)

# use Employee's __init__()
it_1 = IT("James", "Hughes", "32", 5000, "python")

# isinstance(<class_name>, <class_name>)
# issubclass(<class_name>, <class_name>)
```
