---
title: Built-in functions
description: Built-in functions
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

## abs()

## aiter()

- Asynchronous iterator

## all()

- `all(iter)` returns `True` if all of the elements are true values.

```python
all([0, 1, 0]) # False
all([0, 0, 0]) # False
all([1, 1, 1]) # True
```

## any()

- `any(iter)` returns `True` if any element in the iterable is a true value.

```python
any([0, 1, 0]) # True
any([0, 0, 0]) # False
any([1, 1, 1]) # True
```

## anext()

## ascii()

## bin()

## bool()

## breakpoint()

## bytearray()

- To convert the `byte` object into a mutable `bytearray` object, use the built-in `bytearray()` function.
- All the methods and operations you can do on a `bytes` object, you can do on a `bytearray` object too.
- The one difference is that, with the `bytearray` object, you can assign individual bytes using index notation. The assigned value must be an integer between 0–255.

```python
by = b'abcd\x65'
barr = bytearray(by) # barr := b'abcde'
len(barr) # 5
barr[0] = 102
```

## bytes()

- bytes objects are immutable sequences of single bytes.

- bytes literals may also use an *r* prefix to disable the processing of escape sequences.

- Each byte within the byte literal can be an ASCII character or an encoded hexadecimal number from `\x00` to `\xff`. (*1)

```python

# syntax := b''
by = b'abcd\x65' # by = b'abcde' (*1)

<bytes_var> = <str_var>.encode("utf-8")

<str_var> = <bytes_var>.decode("utf-8")

```

## callable()

## chr()

## classmethod()

## compile()

## complex()

## delattr()

## dict()

## dir()

## divmod()

## enumerate()

- `enumerate(iter, start=0)` counts off the elements in the iterable returning 2-tuples containing the count (from start) and each element.

```python
for item in enumerate(['subject', 'verb', 'object']):
    print(item) # (0, 'subject') (1, 'verb') (2, 'object')
```

## eval()

- It evaluates arbitrary strings as python expressions.
- You should only use `eval()` on trusted input.

```python
eval('1 + 1 == 2')
eval('"AAAAA".count("A")')
```

## exec()

## filter()

- `filter(predicate, iter)` returns an iterator over all the sequence elements that meet a certain condition.

- A predicate is a function that returns the truth value of some condition. It must take a single value.

```python
def is_even(x):
    return (x % 2) == 0

list(filter(is_even, range(10))) # [0, 2, 4, 6, 8]
# equal to
list(x for x in range(10) if is_even(x))
```

[Ref](https://docs.python.org/3/howto/functional.html)

## float()

## format()

## frozenset()

## getattr()

## globals()

## hasattr()

## hash()

## help()

## hex()

## id

- `id(<object>)` returns the identity (unique integer) of an object.

- It remains constant during its lifetime.

[Ref](https://www.programiz.com/python-programming/methods/built-in/id)

## input()

## int()

```python
# binary to integer
int('<str>',2)
```

## isinstance()

## issubclass()

## iter()

## len()

## list()

## locals()

## map()

- `map(f, iterA, iterB, ...)` returns an iterator over the sequence.
f(iterA[0], iterB[0]), f(iterA[1], iterB[1]), ...

```python
def upper(s):
    return s.upper()

list(map(upper, ['sentence', 'fragment'])) # ['SENTENCE', 'FRAGMENT']
# equal to
[upper(s) for s in ['sentence', 'fragment']]  # ['SENTENCE', 'FRAGMENT']
```

[Ref](https://docs.python.org/3/howto/functional.html)

## max()

## memoryview()

## min()

## next()

## object()

## oct()

## open()

## ord()

- Given a string representing one Unicode character, return an integer representing the Unicode code point of that character.

```python
ord('a') # 97
```

## pow()

## print()

## property()

## range()

## repr()

## reversed()

## round()

---

## set()

- Unordered collections of unique elements
- Similar to dicts without values
- Based on hash tables
- Creation
  - `set()`
  - `{}`

- **Tip:** use literal declaration {} instead of set().

`set(list) := O(N)`

### Operations

- `<set_name>.add(<item>)`

- `<set_name>.clear()`
- `<set_name>.remove(<item>)` #  if a value doesn’t exist in the set, it raises a KeyError exception.
- `<set_name>.discard(<item>)` # if a value that doesn’t exist in the set, it does nothing. No error; it’s just a no-op.
- `a.pop()` removes an arbitrary element from the set, raising KeyError if the set is empty

- `<set1>.union(<set2>)` or `<set1> | <set2>`
- `<set1>.update(<set2>)` or `<set1> |= <set2>` sets the contents of `set1` to be the union of the elements in `set1` and `set2`
- `<set1>.intersection(<set2>)` or `<set1> & <set2>`
- `<set1>.intersection_update(<set2>)` or `<set1> &= <set2>` similar to the union's
- `<set1>.difference(<set2>)` or `a - b`
- `<set1>.difference_update(<set2>)` or `a -= b` similar to the union's
- `<set1>.symmetric_difference(<set2>)` or `a ^ b`
- `<set1>.symmetric_difference_update(<set2>)` or `a ^= b` similar to the union's
- `<set1>.issubset(<set2>)`
- `<set1>.issuperset(<set2>)`
- `<set1>.isdisjoint(<set2>)`

### Practical consequences of how `dict` works

1. Set elements must be hashable objects.
2. Sets have a significant memory overhead.
3. Membership testing is very efficient.
4. Element ordering depends on insertion order.
5. Adding elements to a set may change the order of other elements.

---

## setattr()

## slice()

## sorted()

- `sorted(iterable, key=None, reverse=False)`

```python
# [9878, 9828, 8442, 7953, 6431, 6213, 2207, 769]
sorted([769, 7953, 9828, 6431, 8442, 9878, 6213, 2207], reverse=True)
```

## staticmethod()

## str()

## sum()

## super()

## tuple()

## type()

## vars()

## zip()

- `zip(iterA, iterB, ...)` takes one element from each iterable and returns them in a tuple.

```python
zip(['a', 'b', 'c'], (1, 2, 3)) # ('a', 1), ('b', 2), ('c', 3)

###

# The shortest is taken.
zip(['a', 'b'], (1, 2, 3)) # ('a', 1), ('b', 2)
```

## `__import__()`
