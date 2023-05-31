---
title: Pydash
description: Pydash
summary: "Updated by Fatma, Mar 29, 2023."
date: 29-03-2023
categories:
  - "Coding"
tags:
  - "Python"
  - "coding"
  - "algorithms"
  - "data structures"
comments: true
---
- It is a kitchen sink of Python utility libraries for doing "stuff" in a functional way.

```python
import pydash as py_

# flatten a nested Python list
py_.flatten([1, 2, [3, [4, 5, [6, 7]]]]) # [1, 2, 3, [4, 5, [6, 7]]]

# flatten nested Python lists
py_.flatten_deep([1, 2, [3, [4, 5, [6, 7]]]]) # [1, 2, 3, 4, 5, 6, 7]

# create an array of values by running each element in the collection through the iteratee
py_.map_([{'name': 'moe', 'age': 40}, {'name': 'larry', 'age': 50}], 'name') # ['moe', 'larry']

# take a function that takes multiple arguments and turn it into a sequence of functions that each take a single argument
curried = py_.curry(lambda a, b, c: a + b + c)
curried(1, 2)(3) # 6

# create an object composed of the picked object properties
py_.pick({'a': 1, 'b': 2, 'c': 3}, 'a', 'b') # {'a': 1, 'b': 2}

# create an object composed of the property paths of obj that are not omitted
py_.omit({'name': 'moe', 'age': 40}, 'age') # {'name': 'moe'}

# execute the iteratee n (here n=3) times, returning a list of the results of each iteratee execution
py_.times(3, lambda index: index) # [0, 1, 2]

# `chain` wraps the list into a chain object
# `without` creates an array with all occurrences of the passed values removed
# `reject` returns the elements of a collection that the predicate does not return truthy for
py_.chain([1, 2, 3, 4]).without(2, 3).reject(lambda x: x > 1).value() # [1]

laptop = {
    "stock": {
        "apple": {"store": {"A": [10,2], "B":[1]}},
        "dell": {"store": {"X": [0]}}
    }
}

# get the value at any depth of a nested object based on the path described by path
py_.get(laptop, "stock.apple.store.A[1]")

# create a list of elements split into groups the length of size
py_.chunk([1, 2, 3, 4, 5], 2) # [[1, 2], [3, 4], [5]]

# get the index of an element in a list
items = [
    {"name":"pencil", "price":1},
    {"name":"notebook", "price":10},
]
filtered_items = lambda item: item["name"] == "notebook"
py_.find_index(items, filtered_items) # 1
```

- For more details: [pydash](https://pydash.readthedocs.io/en/latest/)
