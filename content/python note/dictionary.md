---
title: Dictionary
description: Dictionary
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

- Dictionaries are widely used instead of `if statements` in python.
- If the key is not present, it will raise an exception.
- Dictionaries are also a fundamental part of the Python implementation:
  - module namespaces
  - class and instance attributes
  - function keyword arguments
  where dictionaries are deployed.
- **Tip:** use literal declaration {} instead of dict().
- `dict` objects keep their items in the same order they were introduced with the release of version 3.6.

## Operations

### deletion

- `del <dict_name>['<key>']` # delete a single element
- `<dict_name>.clear()` # delete all elements in the dictionary
- `del <dict_name>` # delete the dictionary

### get

- To handle missing `<key>`:
  - `<dict>.get(<key>, default)`

### joining two dictionaries

- `<dict1>.update(<dict2>)`

### pop

- Remove and return value at `<key>`, or `default` or `None` if missing:
  - `<dict>.pop(<key>, <default_value>)`

### reversing the pairs

```python
DIAL_CODES = [
  (86, 'China'),
  (91, 'India'),
  (1, 'United States'),
  (62, 'Indonesia'),
  (55, 'Brazil'),
  (92, 'Pakistan'),
  (880, 'Bangladesh'),
  (234, 'Nigeria'),
  (7, 'Russia'),
  (81, 'Japan'),
 ]
 
 country_code = {country: code for code, country in DIAL_CODES}
 # {'China': 86, 'India': 91, 'Bangladesh': 880, 'United States': 1, 'Pakistan': 92, 'Japan': 81, 'Russia': 7, 'Brazil': 55, 'Nigeria': 234, 'Indonesia': 62}
```

### setdefault

- If `<key>` in `<dict>`, return `<dict[key]>`; else set `dict[key] = default` and return it:
  - `<dict>.setdefault(<key>, <default_value>)`

```python
for word in words:
  letter = word[0]
  by_letter.setdefault(letter, []).append(word)
```

### update

- `<dict_name>.update({'<key>' : <value>, '<key>' : value})`

## Practical consequences of how `dict` works

1. Keys must be hashable objects.
2. `dicts` have significant memory overhead.
3. Key search is very fast.
4. Key ordering depends on insertion order.
5. Adding items to a `dict` may change the order of existing keys.

## Sorting

- Sorting is rarely done in-place for dicts. (You can delete the item and add it again to make it in-place.)
- There are two ways to sort list dictionary by value:
  - (1) Using lambda function
    - For descending order: `reverse=True`
    - For sorting w.r.t multiple values: Separate by `,` mentioning the correct order
  - (2) Using itemgetter
    - **Performance:** itemgetter performs better than lambda functions in the context of time.
    - **Concise:** itemgetter looks more concise when accessing multiple values than lambda functions.

```python
from operator import itemgetter

lis = [ {"name": "Nandini", "age": 20}, {"name": "Manjeet", "age": 20}, {"name": "Nikhil", "age": 19} ]

print("The list printed sorting by age: ")
print(sorted(lis, key=itemgetter('age')))

print("The list printed sorting by age and name: ")
print(sorted(lis, key=itemgetter('age', 'name')))

print("The list printed sorting by age in descending order: ")
print(sorted(lis, key=itemgetter('age'), reverse=True))
```

```python
lis = [{"name": "Nandini", "age": 20},
       {"name": "Manjeet", "age": 20},
       {"name": "Nikhil", "age": 19}]

print("The list printed sorting by age: ")
print(sorted(lis, key=lambda i: i['age']))

print("The list printed sorting by age and name: ")
print(sorted(lis, key=lambda i: (i['age'], i['name'])))

print("The list printed sorting by age in descending order: ")
print(sorted(lis, key=lambda i: i['age'], reverse=True))
```

## sort by value

```python
###
def value_getter(item):
  return item[1]

sorted(<dict>.items(), key=value_getter)
# equals to
{k: v for k, v in sorted(<dict>.items(), key=lambda item: item[1])}
###
from operator import itemgetter

item = ('Bob','Alice')
getter = itemgetter(0) # 'Bob'
###
intervals = sorted(intervals, key = lambda x : (x[0], -x[1]))
```

## sort by key

-`sorted(<dict>.items())`

## Merging Two Dictionaries

```python
dict1 = {'a': 10, 'b': 8}
dict2 = {'d': 6, 'c': 4}

dict2.update(dict1) # changes made in dict2
# OR
res = {**dict1, **dict2}
# OR
res = dict1 | dict2
```
