---
title: Collections
description: Collections
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

## ChainMap

---

## Counter

- Counter is a special subclass of a dictionary which performs acts the same as a dictionary in most cases.
- You provide a sequence of iterable hashable objects as an argument to the class's constructor.
- Counter inherits the interface of regular dictionaries. However, it doesn't provide a working implementation of `.fromkeys()` to prevent ambiguities.
- If you try to access a missing key, then you get zero instead of a `KeyError`.

### Updating object counts

```python
from collections import Counter

letters = Counter({"i": 4, "s": 4, "p": 2, "m": 1})
letters.update("missouri") # Counter({'i': 6, 's': 6, 'p': 2, 'm': 2, 'o': 1, 'u': 1, 'r': 1})
```

### Finding the most common objects

```python
from collections import Counter

sales = Counter(banana=15, tomato=4, apple=39, orange=30)

sales.most_common(1) # [('apple', 39)]
sales.most_common(2) # [('apple', 39), ('orange', 30)]

# All objects sorted by count
# [('apple', 39), ('orange', 30), ('banana', 15), ('tomato', 4)]
sales.most_common() # OR
sales.most_common(None) # OR
sales.most_common(20)
```

- A subclass of a dict for counting hashable objects.
  - It is a collection where elements are stored as dictionary keys and their counts are stored as dictionary values.
- O(N) := construct
- O(1) := individual element operations

```python
s1_counter = {}
for ch in s1:
    s1_counter[ch] = s1_counter.get(ch, 0) + 1
```

### Combining two dictionaries

```python
from collections import Counter
  
ini_dictionary1 = Counter({'nikhil': 1, 'akash' : 5, 'manjeet' : 10, 'akshat' : 15})
ini_dictionary2 = Counter({'akash' : 7, 'akshat' : 5, 'm' : 15})
  
print ("initial 1st dictionary", str(ini_dictionary1))
print ("initial 2nd dictionary", str(ini_dictionary2))
  
final_dictionary = ini_dictionary1 + ini_dictionary2
# OR
# final_dictionary =  {x: ini_dictionary1.get(x, 0) + ini_dictionary2.get(x, 0) for x in set(ini_dictionary1).union(ini_dictionary2)}
  
print ("final dictionary", str(final_dictionary))
```

---

## defaultdict

- Built-in `defaultdict` creates one, you pass a type or function for generating the default value for each slot in the dict.

```python
from collections import defaultdict

by_letter = defaultdict(list)
for word in words:
  by_letter[word[0]].append(word)
```

---

## deque (Double-ended queue)

- You can access, insert, or remove elements from the beginning or end of a list in `O(1)`.
- If you are constantly adding and removing items from the ends of a list, a `deque` works faster.

```python
from collections import deque

# create an empty deque
deque()

# you can pass any iterable as an input, such as a string and a list of objects.
deque('abc') # ['a', 'b', 'c']
deque([{'data': 'a'}, {'data': 'b'}]) # [{'data': 'a'}, {'data': 'b'}]

llist = deque("abcde")
# from the beginning
llist.appendleft('z') # deque(['z', 'a', 'b', 'c', 'd', 'e'])
llist.popleft() # deque([a', 'b', 'c', 'd', 'e'])
# from the end
llist.append('z') # deque(['a', 'b', 'c', 'd', 'e', 'z'])
llist.pop() # deque([a', 'b', 'c', 'd', 'e'])

##
# the size can be limited so it discards items from the opposite end when it is full
dq = deque(range(10), maxlen=10) # [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
dq.rotate(3) # [7, 8, 9, 0, 1, 2, 3, 4, 5, 6]
dq.rotate(-4) # [1, 2, 3, 4, 5, 6, 7, 8, 9, 0]
dq.extendleft([10, 20, 30, 40]) # [40, 30, 20, 10, 1, 2, 3, 4, 5, 6]
```

- `insert` is computationally expensive compared with append, because references to subsequent elements have to be shifted internally to make room for the new element. If you need to insert elements at both the beginning and end of a sequence, you may wish to explore `collections.deque`, a double-ended queue, for this purpose.

```python
from collections import deque

# DEQUE built-in functions
# append(elem)
# appendLeft(elem)
# clear() removes all the elements
# copy
# count(element)
# extend() adds more elements from an iterable
# extendLeft() adds more elements from an iterable

def search(lines, pattern, history=5):
  # When the deque has reached the maxlen, if an
  # element is added to the left size one element
  # is removed from the right side, and vice versa for
  # the right.
  previous_lines = deque(maxlen=history)
  for line in lines:
    if pattern in line:
      yield line, previous_lines
    previous_lines.append(line)
  

if __name__ == "__main__":
  with open('somefile.txt') as f:
    for line, prevlines in search(f, 'python', 5):
      for pline in prevlines:
        print(pline, end='')
      print(line, end='')
      print('-')*20
```

- The deque initializer takes the following two optional arguments:
  1. `iterable` holds an iterable that provides the initialization data.
  2. `maxlen` holds an integer number that specifies the maximum length of the deque.

- `.remove()` lets you delete items by value, while `del` removes items by index.

- Even though deque objects support indexing, they don’t support slicing. In other words, you can’t extract a slice from an existing deque using the slicing syntax, [start:stop:step], as you would with a regular list.

```python
from collections import deque

numbers = deque([1, 2, 3, 4, 5])

numbers[1:3]
# Traceback (most recent call last):
#   File "<stdin>", line 1, in <module>
# TypeError: sequence index must be an integer, not 'slice'
```

- `list` is based on arrays, and `deque` is based on a doubly linked list.

operation                                       deque list
Accessing arbitrary items through indexing      O(n)    O(1)
Popping and appending items on the left end     O(1)    O(n)
Popping and appending items on the right end    O(1)    O(1) + reallocation
Inserting and deleting items in the middle      O(n)    O(n)

### extend

```python
from collections import deque

numbers = deque([1, 2])

numbers.extend([3, 4, 5]) # [1, 2, 3, 4, 5]
numbers.extendleft([-1, -2, -3, -4, -5]) # [-5, -4, -3, -2, -1, 1, 2, 3, 4, 5]
```

### rotate

```python
from collections import deque

pages = deque(maxlen=3)

ordinals = deque(["first", "second", "third"])
ordinals.rotate() # ['third', 'first', 'second']
ordinals.copy() # shallow copy
ordinals.index('first')
ordinals.count('second')
ordinals.rotate(2) # ['first', 'second', 'third']
ordinals.rotate(-2) # ['third', 'first', 'second']
ordinals.rotate(-1) # ['first', 'second', 'third']
ordinals.reverse() # ['third', 'second', 'first']
ordinals * 2 # [ 'first', 'second', 'third', 'first', 'second', 'third' ]
ordinals.clear()
```

[Ref 1](https://realpython.com/linked-lists-python/), [Ref 2](https://docs.python.org/2/library/collections.html#collections.deque)

---

## namedtuple

- They can be used wherever regular tuples are used, and they add the ability to access fields by name instead of position index.

```python
from collections import namedtuple

##

# collections.namedtuple(typename, field_names, *, rename=False, defaults=None, module=None)
Point = namedtuple( 'Point', [ 'x', 'y' ] )

##

Task = namedtuple( 'Task', [ 'summary', 'owner', 'done', 'id' ])
t_task = Task( 'do something', 'okken', True, 21 )

# _asdict():= returns a dictionary of which keys are the fields of the named tuple and the values are the values corresponding to them
t_dict = t_task._asdict()
t_after = t_before._replace(id=10, done=True) # changes passed in fields

```

[Ref](https://docs.python.org/3/library/collections.html#namedtuple-factory-function-for-tuples-with-named-fields)

## OrderedDict

```python
from collections import OrderedDict
```

## UserDict

- .

## UserList

- .

## UserString

- .
