---
title: Design patterns
description: Design patterns
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
- A design pattern offers a widely applicable and reusable solution for addressing common problems in software design.
- It illustrates how classes or objects interact and relate to each other.
- It is programming language-independent, so it represents thinking.
- We should understand the intention and use of each pattern.

## 1. Creational patterns

- They instantiate classes or create objects.

### 1.1 Abstract factory

- Create entire product families without specifying their concrete classes

---

### 1.2 Factory

- Create product objects without specifying their concrete classes

```python
class FrenchLocalizer:
    def __init__(self):
        self.translations = {"car": "voiture", "bike": "bicyclette", "cycle":"cyclette"}
 
    def localize(self, msg):
        return self.translations.get(msg, msg)
 
class SpanishLocalizer:
    def __init__(self):
        self.translations = {"car": "coche", "bike": "bicicleta", "cycle":"ciclo"}
 
    def localize(self, msg):
        return self.translations.get(msg, msg)
 
class EnglishLocalizer:
    def localize(self, msg):
        return msg
 
def Factory(language ="English"):
    localizers = {
        "French": FrenchLocalizer,
        "English": EnglishLocalizer,
        "Spanish": SpanishLocalizer,
    }
 
    return localizers[language]()

if __name__ == "__main__":
    f = Factory("French")
    e = Factory("English")
    s = Factory("Spanish")
 
    message = ["car", "bike", "cycle"]
 
    for msg in message:
        print(f.localize(msg))
        print(e.localize(msg))
        print(s.localize(msg))
```

[Code](https://www.geeksforgeeks.org/factory-method-python-design-patterns)

---

### 1.3 Builder

- Construct complex objects step-by-step

---

### 1.4 Prototype

- Copy existing objects without making your code dependent on their classes

---

### 1.5 Singleton

- Ensure that a class has only one instance, while providing a global access point to this instance

---

## 2. Structural patterns

### 2.1 Adapter

- Allow objects with incompatible interfaces to collaborate

```python
class Elf:
  def nall_nin(self):
    print('Elf')
  
class Dwarf:
  def estver_narho(self):
    print('Dwarf')

class Human:
  def ring_mig(self):
    print('Human')

class MinionAdapter:
  _initialised = False

  def __init__(self, minion, **adapted_methods):
    self.minion = minion

    for key,value in adapted_methods.items():
      func = getattr(self.minion, value)
      self.__setattr__(key,func)
    self._initialised = True

  def __getattr__(self, attr):
    return getattr(self.minion, attr)
  
  def __setattr__(self, key, value):
    if not self._initialised:
      super().__setattr__(key, value)
    else:
      setattr(self.minion, key, value)

if __name__ == "__main__":
  minions =  [ MinionAdapter(Elf(), call_me='nall_nin'), MinionAdapter(Dwarf(), call_me='estver_narho'), MinionAdapter(Human(), call_me='ring_mig') ]

  for minion in minions:
    minion.call_me()
```

---

### 2.2 Bridge

- Split a large class or a set of closely related classes into two separate hierarchies-abstraction and implementation- which can be developed independently of each other

---

### 2.3 Composite

- Compose objects into tree structures and then work with these structures as if they were individual objects

---

### 2.4 Decorator

- Attach new behaviours to objects by placing these objects inside special wrapper objects that contain the behaviours

---

### 2.5 Facade

- Provide a simplified interface to a library, a framework, or any other complex set of classes

```python
class Elf:
  def nall_nin(self):
    print('Elf')
  
class Dwarf:
  def estver_narho(self):
    print('Dwarf')

class Human:
  def ring_mig(self):
    print('Human')

class MinionAdapter:
  _initialised = False

  def __init__(self, minion, **adapted_methods):
    self.minion = minion

    for key,value in adapted_methods.items():
      func = getattr(self.minion, value)
      self.__setattr__(key,func)
    self._initialised = True

  def __getattr__(self, attr):
    return getattr(self.minion, attr)
  
  def __setattr__(self, key, value):
    if not self._initialised:
      super().__setattr__(key, value)
    else:
      setattr(self.minion, key, value)

class MinionFacade:
  minion_adapters = None

  @classmethod
  def create_minions(cls):
    cls.minion_adapters = [
      MinionAdapter(Elf(), call_me='nall_nin'),
      MinionAdapter(Dwarf(), call_me='estver_narho'),
      MinionAdapter(Human(), call_me='ring_mig'),
    ]

  @classmethod
  def summon_minions(cls):
    print('Summoning minions...')
    for adapter in cls.minion_adapters:
      adapter.call_me()

if __name__ == "__main__":
  MinionFacade.create_minions()
  MinionFacade.summon_minions()
```

### 2.6 Flyweight

- Fit more objects into the available amount of RAM by sharing common parts of state between multiple objects instead of keeping all of the data in each object

---

### 2.7 Proxy

- Provide a substitute or placeholder for another object

---

## 3. Behavioral patterns

### 3.1 Chain of responsibility

- Pass requests along a chain of handlers

---

### 3.2 Command

- Turn a request into a stand-alone object that contains all information about the request

---

### 3.3 Iterator

- Traverse elements of a collection without exposing its underlying representation

---

### 3.4 Mediator

- Reduce chaotic dependencies between objects
- It restricts direct communication between the objects and forces them to collaborate only via a mediator object.

---

### 3.5 Memento

- Save and restore the previous state of an object without revealing the details of its implementation

---

### 3.6 Observer

- Define a subscription mechanism to notify multiple objects about any events that happen to the object they're observing

```python
class Elf:
  def nall_nin(self):
    print('Elf')
  
class Dwarf:
  def estver_narho(self):
    print('Dwarf')

class Human:
  def ring_mig(self):
    print('Human')

class Observer:
  def update(self, obj, *args, **kwargs):
    raise NotImplementedError

class Observable:
  def __init__(self):
    self._observers = []
  
  def add_observer(self, observer):
    self._observers.append(observer)
  
  def remove_observer(self, observer):
    self._observers.remove(observer)
  
  def notify_observer(self, *args, **kwargs):
    for observer in self._observers:
      observer.update(self, *args, **kwargs)

class MinionAdapter(Observable):
  _initialised = False

  def __init__(self, minion, **adapted_methods):
    super().__init__()
    self.minion = minion

    for key,value in adapted_methods.items():
      func = getattr(self.minion, value)
      self.__setattr__(key,func)
    self._initialised = True

  def __getattr__(self, attr):
    return getattr(self.minion, attr)
  
  def __setattr__(self, key, value):
    if not self._initialised:
      super().__setattr__(key, value)
    else:
      setattr(self.minion, key, value)
      self.notify_observer(key=key, value=value)

class MinionFacade:
  minion_adapters = None

  @classmethod
  def create_minions(cls):
    cls.minion_adapters = [
      MinionAdapter(Elf(), call_me='nall_nin'),
      MinionAdapter(Dwarf(), call_me='estver_narho'),
      MinionAdapter(Human(), call_me='ring_mig'),
    ]

  @classmethod
  def summon_minions(cls):
    print('Summoning minions...')
    for adapter in cls.minion_adapters:
      adapter.call_me()

  @classmethod
  def monitor_elves(cls, observer):
    cls.minion_adapters[0].add_observer(observer)
    print('Added an observer to the Elves!')

  @classmethod
  def change_elves_name(cls, new_name):
    print('Changing the Elves name ...')
    cls.minion_adapters[0].name = new_name
    print('Elves name changed!')

class EvilOverlord(Observer):
  def update(self, obj, *args, **kwargs):
    print('The Evil Overlord received a message!')
    print(f'Object: {obj}, Args: {args}, Kwargs: {kwargs}')

if __name__ == "__main__":
  overlord = EvilOverlord()

  MinionFacade.create_minions()
  MinionFacade.monitor_elves(overlord)
  MinionFacade.change_elves_name('Elrond')
```

---

### 3.7 State

- Alter an object behaviour when its internal state changes

---

### 3.8 Strategy

- Define a family of algorithms, put each of them into a separate class, and make their objects interchangeable

---

### 3.9 Template

- Define the skeleton of an algorithm in the superclass but lets subclasses override specific steps of the algorithm without changing its structure

---

### 3.10 Visitor

- Separate algorithms from the objects on which they operate

---
