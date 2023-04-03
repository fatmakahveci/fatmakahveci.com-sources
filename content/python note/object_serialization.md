---
title: Object serialization
description: Object serialization
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
- Serialization refers to the process of converting an object in memory to a byte stream that can be stored on disk or sent over a network.
- Later on, this character stream can then be retrieved and de-serialized back to a Python object.
- Pickling is not to be confused with compression!
  - *Pickling* is the conversion of an object from one representation (data in Random Access Memory (RAM)) to another (text on disk).
  - *Compression* is the process of encoding data with fewer bits, to save disk space.

## Marshal

- Serializing data means converting it into a string of bytes and later reconstructing it from such a string.
- If the data is composed entirely of fundamental Python objects, the fastest way to serialize the data is by using the marshal module.
- It contains functions that can read and write Python values in a binary format.
- It supports reading and writing the "pseudo-compiled" code for Python modules of .pyc files.
- It doesn't support all Python object types.
- The following types are supported: booleans, integers, floating point numbers, complex numbers, strings, bytes, bytearrays, tuples, lists, sets, frozensets, dictionaries, and code objects, where it should be understood that tuples, lists, sets, frozensets and dictionaries are only supported as long as the values contained therein are themselves supported.

[Ref](https://www.geeksforgeeks.org/marshal-internal-python-object-serialization/)

## pickle

- It is used for implementing binary protocols for serializing and de-serializing a Python object structure.
  - Pickling: It is a process where a Python object hierarchy is converted into a byte stream.
  - Unpickling: It is the inverse of the Pickling process where a byte stream is converted into an object hierarchy.
- Module Interface
  - dumps() – This function is called to serialize an object hierarchy.
  - loads() – This function is called to de-serialize a data stream.
- For user-defined classes, pickle should be preferred rather than marshal for object serialization.

- When (not) to use it

- How to compress pickled objects

- Multiprocessing

[Ref](<https://www.datacamp.com/community/tutorials/pickle-python-tutorial>), [Ref](<https://www.geeksforgeeks.org/pickle-python-object-serialization/?ref=rp>)

## JSON

- It works with standard JSON files.
- The JSON module and XML are good choices if we want interoperability among different languages.
- Types are only
  - `null`
  - `boolean`
  - `numeric`
  - `string`
  - `array`
  - `object`

[Ref](https://www.geeksforgeeks.org/modules-available-for-serialization-and-deserialization-in-python/?ref=rp)
