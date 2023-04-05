---
title: Sequences
description: Sequences
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

## Operations

- Sequences share a rich set of common operations including
  - iteration,
  - slicing,
  - sorting, and
  - concatenation.

### Slicing

```python
s = 'bicycle'
s[::3] # bye
s[::-2] # eccb

##

invoice = """
0.....6.................................40........52...55........
1909 Pimoroni PiBrella $17.50 3 $52.50
1489 6mm Tactile Switch x20 $4.95 2 $9.90
1510 Panavise Jr. - PV-201 $28.00 1 $28.00
1601 PiTFT Mini Kit 320x240 $34.95 1 $34.95
"""
DESCRIPTION = slice(6, 40)
line_items = invoice.split('\n')[2:]
for item in line_items:
  print(item[DESCRIPTION])

## Assigning to slices
l = list(range(10)) # 0 1 2 3 4 5 6 7 8 9
l[2:5] = [20, 30] # 0 1 20 30 5 6 7 8 9
del l[5:7] # 0 1 20 30 5 8 9
l[3::2] = [11, 22] # 0 1 20 11 5 22 9
# l[2:5] = 100 # not allowed if the target is sliced the right-hand side must be iterable even if it has just one item
l[2:5] = [100] # 0 1 100 22 9
```

- [] operator can take
  - multiple indexes _or_
  - slices separated by commas.

---

## Sequence types

- Sequences can be categorized as either container or flat.
  - Container sequences can hold items of different types, such as `list`, `tuple`, and `collections.deque`. They hold references to the objects they contain.
  - Flat sequences can hold items of one type. `str`, `bytes`, `bytearray`, `memoryview`, and `array.array`. They store the value of each item within its own memory space, not as distinct objects. They are limited to holding primitives values like `chars`, `bytes`, `numbers`, etc.

- Sequences can also be categorized as either mutable or immutable.
  - Mutable sequences can be modified after they are created, such as `list`, `bytearray`, `array.array`, `collections.deque`, `memoryview`, `bitarray`.
  - Immutable sequences cannot be modified after they are created, such as `tuple`, `str`, `bytes`.

---

### array.array

- If all you want to put in the list are numbers, an array.array is more efficient than a list.
- It supports all mutable sequence operations.
  - `.pop`
  - `.insert`
  - `.extend`
  - `.frombytes` fast loading
  - `.tofile` fast saving

```python
from array import array
from random import random

# creates an array of double-precision floats from any iterable object, in this case, a generator
floats = array('d', (random() for i in range(10**7)))
floats2 = array('d')

# save the array to a binary file
fp = open('floats.bin', 'wb')
floats.tofile(fp)
fp.close()

# reads from the binary file
fp = open('floats.bin', 'rb')
floats2.fromfile(fp, 10**7)
fp.close()
```

---

### bitarray

- `pip install bitarray`

- It is an efficient way of representing bools in an array.

```python
from bitarray import bitarray

arr = bitarray()      

arr.append(False) # bitarray(0)
arr.append(True) # bitarray(1)

arr = bitarray(2**5) # creates an empty bit array of size 32
bitarray('11011011') # declares a bitarray using string
```

#### Bitwise operators

- `&, |, ^, &=, |=, ^=, ~`
- There is no sign bit and `unsigned right shift operator (>>>)` in Python.
- They are to implement algorithms such as
  - compression
  - encryption
  - error detection
- Bit masks pack information on a single byte.
- `(42).bit_length()` # 6

#### Functions

- `all()` is `True` when all bits in the array are `True`.
- `any()` is `True` when any bit in the array is `True`.
- `append(item, /)` appends the truth value `bool(item)` to the end of the bitarray.
- `bytereverse()` reverses the bit order in place.
- `clear()` empties the bitarray.
- `copy()` copies the bitarray.
- `count(value=True, start=0, stop=<end of array>, /)` counts the frequency of a bool value.
- `endian()` # 'big' # bitarray(endian='little')
- `extend(iterable or string, /)` extends the bitarray.
- `fill()` adds 0s to the end of bitarray to make it a multiple of 8.
- `array.frombytes(b'A')` # bitarray('01000001')
- `index(value, start=0, stop=<end of array>, /)` finds the index of the first occurrence of the given bool value int.
- `insert(index, value, /)` inserts a bool value in the given index.
- `invert(index=<all bits>)` inverts all bits in place.
- `itersearch(bitarray, /)` searches for the given bitarray.
- `length()` gives the length of the bitarray.
- `pop(index=-1, /)` deletes and returns the ith element.
- `remove(value, /)` remove the first occurrence of given bool value.
- `reverse()` reverses the order of bits in place.
- `setall(0)` sets all elements in a to 0.
- `sort(reverse=False)` sorts the bits in place.
- `a.tobytes()` # b'A'

---

### bytearray

---

### bytes

- To define a bytes variable, just prepend a `b` to the string.

### bytes vs str

1. `str` is represented internally as a sequence of Unicode codepoints. You can declare a `str` variable without prepending the string with `u`.

2. `bytes` is a binary serialization format represented by a sequence of 8-bit integers that is fit for storing data on the filesystem or sending it across the Internet. That is why you can only create bytes containing ASCII literal characters.

- `bytes := str.encode()`
- `str := bytes.decode()`

---

### collections.deque

---

### lists

- If you keep a big array an array is much more efficient because an array does not hold full-fledged float objects. It only holds the packed bytes representing their machine values, just like an array in the `C` language.

#### Lists of lists

```python
board = [['_'] * 3 for i in range(3)] # [['_', '_', '_'], ['_', '_', '_'], ['_', '_', '_']]
# equals to
board = []
for i in range(3):
  row = ['_'] * 3   # each iteration builds a new row and 
  board.append(row) # appends it to board.

##

# a wrong case
weird_board = [['_'] * 3] * 3 # this is made of three references to the same inner list.
weird_board[1][2] = 'O' # [['_', '_', 'O'], ['_', '_', 'O'], ['_', '_', 'O']]
# equals to
row = ['_'] * 3
board = []
for i in range(3):
  board.append(row) # the same row is appended 3 times to the board.
```

- In the wrong case, there is a list with three references to the same list.

---

### memoryview

- `memoryview` references the object.
- It is important for large data sets.
- It allows direct read and writes access to an object's byte-oriented data without needing to copy it first.
- It allows you to share memory between data structures like PIL images, SQLite databases, and NumPy arrays without first copying.
- It allows to access the internal data of an object that supports the buffer protocol without copying.
- `memoryview.cast`

```python
# Create a random byte array
rarray = bytearray('XYZ', 'utf-8')

# Get memory view
mview = memoryview(rarray)

# Print memory view's 0th Index
print(mview[0])

# Create a list of the memory view
print(list(mview[0:3]))

# Create a tuple of the memory view
print(tuple(mview[0:3]))

# Update a value of the memory view
mview[2] = 70

##

numbers = array.array('h', [-2, -1, 0, 1, 2])

# build memoryview from array of 5 short signed integers (typecode 'h')
memv = memoryview(numbers)

len(memv) # 5

# memv sees the same 5 items in the array
memv[0] # -2

# create memv_oct by casting the elements of memv to type code 'B' (unsigned char)
memv_oct = memv.cast('B')

# export elements of memv_oct as list for inspection
memv_oct.tolist() # [254, 255, 255, 255, 0, 0, 1, 0, 2, 0]

# assign value 4 to byte offset 5
memv_oct[5] = 4

# a 4 is in the most significant byte of a 2-byte unsigned integer is 1024.
numbers
```

- It takes a single parameter `<object>`.

[Ref](https://www.geeksforgeeks.org/memoryview-in-python/)

---

### str

#### String representation

```python
class Vector:

  def __init__(self, x=0, y=0):
    self.x = x
    self.y = y

  def __repr__(self):
    return 'Vector(%r, %r)' % (self.x, self.y)
```

- If we don't implement `__repr__`, vector instances will be shown like `<Vector object at 0x10e100070>`.
- `__str__` is called by the `str()` constructor and implicitly used by the print function.
  - It should return a string suitable for display to end-users.
- **If you only implement one of `__repr__` or `__str__`, choose the first because Python will call it a fallback.**

---

### tuples

- Immutable list and records with no field names.

```python
# immutable list example
# latitude and longitude of Los Angeles International Airport (LAX)
lax_coordinates = (33.9425, -118.408056)

# the most visible form of tuple unpacking
latitude, longitude = lax_coordinates

# unpacking with a star
t = divmod(20, 8)
a, b, rest = range(2) # 1, 2, []
a, b, rest = range(5) # 1, 2, [3, 4, 5]

import os
_, file_name = os.path.split('/home/luciano/.ssh/idrsa.pub') # filename = idrsa.pub
```

- Each item in the tuple holds the data for one field.
- The position of the item gives its meaning.

```python
# data example
traveler_ids = [('USA', '4323412'), ('BRA', '2314233'), ('ESP', '3241235')]
for country, _ in traveler_ids: # USA BRA ESP
    print(country)

for passport in sorted(traveler_ids): # USA/4323412 BRA/2314233 ESP/3241235
    print('%s/%s' % passport)

metro_areas = [ ('Tokyo', 'JP', 36.933, (35.689722, 139.691667)),
                ('Delhi NCR', 'IN', 21.935, (28.613889, 77.208889)),
                ('Mexico City', 'MX', 20.142, (19.433333, -99.133333)),
                ('New York-Newark', 'US', 20.104, (40.808611, -74.020386)),
                ('Sao Paulo', 'BR', 19.649, (-23.547778, -46.635833)), 
              ]

fmt = '{:15} | {:9.4f} | {:9.4f}'
for name, cc, pop, (latitude, longitude) in metro_areas:
    if longitude <= 0:
        print(fmt.format(name, latitude, longitude))
```

- Putting mutable items in tuples is not a good idea.

## Sort

```python
my_list = [('b', 4), ('d', 1), ('e', 6), ('m', 2)]
my_list.sort(key=lambda s:s[1])
```

```python
my_tup_lis = [(2, 4), (9, 16), (1, 12), (5, 4)]
mul_sort = sorted(my_tup_lis, key=lambda t: (t[1], t[0]))
```

---

### namedtuple

- It helps to debug.
- They use less memory than regular objects because they store attributes in a per-instance `__dict__`.
- Two parameters are required to create a named tuple:
  - class name
  - a list of field names
    - it can be given as
      - an iterable of strings _or_
      - a single space-delimited string.
- Additional attributes of a named tuple in comparison to a tuple:
  - Class attribute
    - `_fields`
      - a tuple with the field names of the class
  - Class method
    - `_make(iterable)`
      - instantiate a named tuple from an iterable
        - `City._make(delhi_data) <==> City(*delhi_data)`
    - `_asdict()`
      - returns a `collections.OrderedDict`

#### namedtuple example

```python
from collections import namedtuple
from random import choice


Card = namedtuple('Card', ['rank', 'suit'])

class FrenchDeck:
 ranks = [ str(n) for n in range(2, 11) ] + list('JQKA')
 suits = 'spades diamonds clubs hearts'.split()

 def __init__(self):
  self._cards = [ Card(rank, suit) for suit in self.suits
           for rank in self.ranks ]

 def __len__(self):
  return len(self._cards)

 def __getitem__(self, position):
  return self._cards[position]

def spades_high(card):
 rank_value = FrenchDeck.ranks.index(card.rank)
 return rank_value * len(suit_values) + suit_values[card.suit]


if __name__ == "__main__":

 my_card = Card('7', 'diamonds') # Card(rank='7', suit='diamonds')
 deck = FrenchDeck()
 print(len(deck)) # 52
 print(deck[0]) # Card(rank='2', suit='spades')
 choice(deck) # i.e. Card(rank='3', suit='hearts')

 suit_values = dict(spades=3, hearts=2, diamonds=1, clubs=0)
 for card in sorted(deck, key=spades_high):
  print(card) # Card(rank='2', suit='clubs') Card(rank='2', suit='hearts') , ..., Card(rank='A', suit='spades')

 deck[12::13] # [start:stop:step]
 #[Card(rank='A', suit='spades'), Card(rank='A', suit='diamonds'), Card(rank='A', suit='clubs'), Card(rank='A', suit='hearts')]

 ## 

 City = namedtuple('City', 'name country population coordinates')
 tokyo = City('Tokyo', 'JP', 36.933, (35.689722, 139.691667))
  ```
