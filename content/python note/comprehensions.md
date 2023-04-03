---
title: Comprehensions
description: Comprehensions
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

## Dict comprehensions

- They transform one dictionary into another one.
- They can serve as alternatives to `for loop` and `lambda function`.
- In contrast to the list and set comprehensions, it needs two expressions separated with a colon followed by the usual `for` and `if` clauses.

```python
dict_1 = {'a': 1, 'b':2}
double_dict = {k:v*2 for (k,v) in dict_1.items()} # {'a':2, 'b':4}

dict_1_keys = {k*2:v for (k,v) in dict_1.items()} # {'aa':1, 'bb':2}
```

---

- Not all for loops can be written as a dictionary, but all dictionary comprehension can be written with a for loop.

```python
numbers = range(10)

new_dict_comp = {n:n**2 for n in numbers if n%2 == 0} # {0: 0, 2: 4, 4: 16, 6: 36, 8: 64}
```

---

- if condition

```python
dict1 = {'a': 1, 'b': 2, 'c': 3, 'd': 4, 'e': 5, 'f':6}

dict1_tripleCond = {k:v for (k,v) in dict1.items() if v>2 if v%2 == 0 if v%3 == 0}

# equals to

dict1_tripleCond = {}

for (k,v) in dict1.items():
    if (v>=2 and v%2 == 0 and v%3 == 0):
            dict1_tripleCond[k] = v
```

---

- if-else condition

```python
dict1 = {'a': 1, 'b': 2, 'c': 3, 'd': 4, 'e': 5, 'f':6}

dict1_tripleCond = {k:('even' if v%2==0 else 'odd') for (k,v) in dict1.items()}
```

---

- nested

```python
nested_dict = {'first':{'a':1}, 'second':{'b':2}}
float_dict = {outer_k: {float(inner_v) for (inner_k, inner_v) in outer_v.items()} for (outer_k, outer_v) in nested_dict.items()}
```

## List comprehensions

- A list comprehension provides a compact way of mapping a list into another list by applying a function to each of the elements of the list.

- Since the introduction of list comprehensions and generator expressions, `map` and `filter` functions are not as important.

```python

# list comprehensions
list(map(fact, range(6)))
# equals to
[fact(n) for i in range(6)]

#lambda is unnecessary
list(map(factorial, filter(lambda n: n % 2, range(6))))
# equals to
[factorial(n) for n in range(6) if n % 2]
```

```python
# listcomps and readability
symbols = '%$@#!"
codes = [ord(symbol) for symbol in symbols]

# listcomps do not leak their variables
x = 'ABC'
dummy = [ord(x) for x in x]
# x = 'ABC' dummy = [65, 66, 67]

# listcomps vs. map and filter
beyond_ascii = [ord(s) for s in symbols if ord(s) > 127]
# equals to
beyond_ascii = list(filter(lambda c: c > 127, map(ord, symbols)))

# cartesian products
colours = ['black', 'white']
sizes = ['S', 'M', 'L']
tshirts = [(colour, size) for colour in colours for size in sizes]

# tuple
a1=['red', 'green', 'blue']
b1=[0,1,2]
a2=[(a,b) for a in a1 for b in b1]

# zip
l1=['red', 'green', 'blue']
l2=[0,1,2]
l3=[(n1,n2) for n1,n2 in zip(l1,l2)]
```

## Set comprehensions

```python
# <set_comp> = {<expr> for <value> in <collection> if <condition>}

###
s1={n for n in range(1,11) if n%2==0}
print (s1) #Output:{2, 4, 6, 8, 10}
###
s1={n*n for n in range(1,11)}
print (s1) #Output: {64, 1, 4, 36, 100, 9, 16, 49, 81, 25}
###
# tuple
s={(n,n*n) for n in range(1,11) if n%2==0}
print (s)#Output:{(6, 36), (4, 16), (10, 100), (2, 4), (8, 64)}
```
