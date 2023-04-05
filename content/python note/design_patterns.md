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
## Abstract factory

---

## Adapter

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

## Bridge

---

## Builder

---

## Chain of responsibility

---

## Command

---

## Composite

---

## Decorator

---

## Facade

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

---

## Factory

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

[Ref](https://www.geeksforgeeks.org/factory-method-python-design-patterns/`)

---

## Flyweight

---

## Interpreter

---

## Iterator

---

## Mediator

[Ref](https://www.youtube.com/watch?v=65hdyehA3zY&ab_channel=AnthonyFerrara)

---

## Memento

---

## Observer

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

## Prototype

---

## Proxy

---

## Singleton

---

## State

---

## Strategy

---

## Template

---

## Visitor

---
