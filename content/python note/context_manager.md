---
title: Context Managers and the `with` statement
description: Context Managers and the `with` statement
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
- They simplify resource management patterns by abstracting their functionality.

## Creating a context manager

- Context managers can be written using classes or functions (with decorators).

### i. Using classes

- User needs to ensure that the class has the methods:
  - `__enter__` returns the resource that needs to be managed.
  - `__exit__` does not return anything, but performs the cleanup operations.

```python
"""
init method called
enter method called
with statement block
exit method called
"""

class ContextManager():
  def __init__(self):
    print("init method is called")

  def __enter__(self):
    print("enter method is called")
    return self

  def __exit__(self, exc_type, exc_value, exc_traceback):
    print("exit method is called")

with ContextManager() as manager:
  print("with statement block")
```

### ii. Using decorators

```python
"""
Enter method called
with statement block
Exit method called 
"""
from contextlib import contextmanager

@contextmanager
def ContextManager():

  print("Enter method called")

  yield

  print("Exit method called")

with ContextManager as manager:
  print("with statement block")
```

---

## File management using a context manager

```python
class FileManager():
    def __init__(self, filename, mode):
        self.filename = filename
        self.mode = mode
        self.file = None
          
    def __enter__(self):
        self.file = open(self.filename, self.mode)
        return self.file
      
    def __exit__(self, exc_type, exc_value, exc_traceback):
        self.file.close()
  
# loading a file 
with FileManager('test.txt', 'w') as f:
    f.write('Test')
  
print(f.closed) # True
```

---

## Database connection management with a context manager

```python
from pymongo import MongoClient

class MongoDBConnectionManager():
    def __init__(self, hostname, port):
        self.hostname = hostname
        self.port = port
        self.connection = None
    
    def __enter__(self):
        self.connection = MongoClient(self.hostname, self.port)
        return self
  
    def __exit__(self, exc_type, exc_value, exc_traceback):
        self.connection.close()

with MongoDBConnectionManager('localhost', '27017') as mongo:
  collection = mongo.connection.SampleDb.test
  data = collection.find({'_id': 1})
  print(data.get('name'))
```

---

- `with` ensures that open file descriptors are closed automatically after program execution leaves the context of the `with` statement.

```python
with open('hello_world.txt', 'w') as f:
  f.write('hello, world!')
```

---

- `with` statement is used effectively in `threading.Lock` class.

```python
some_lock = threading.Lock()

# USE THIS
with some_lock:
  ...

# INSTEAD OF THIS
some_lock.acquire()
try:
  ...
finally:
  some_lock.release()
```
