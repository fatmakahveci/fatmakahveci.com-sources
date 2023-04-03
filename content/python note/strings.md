---
title: Strings
description: Strings
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
- Encodings convert code points into bytes.
- There are many different character encodings.
- UTF-8 is the current gold standard of Unicode encoding.

## ASCII

- It stores English characters as numbers ranging from 0 to 127.
  - A := 65
  - a:= 97, etc.

## Unicode

- It is a system designed to represent every character from every language.
- It represents each letter, character, or ideograph as a 4-byte number.
  - An ideogram or ideograph is a graphic symbol that represents an idea or concept, independent of any particular language, and specific words or phrases.

### UTF-32

- 32 bits:= 4 bytes per each character
- Finding the Nth character in constant time.

### UTF-16

- 16 bits:= 2 bytes per each character
- Finding the Nth character in constant time.

### UTF-8

- A variable-length encoding system for Unicode.
- Different characters take up a different number of bytes.
  - ASCII:= 1 byte per each character
  - Extended Latin:= 2 bytes per each character
  - Chinese:= 3 bytes per each character, etc.
- Finding the Nth character in O(N) time.

```python
val = "español"

# Encoding is like a kind of decryption key.
val_utf8 = val.encode('utf-8') # b'espa\xc3\xb1ol'
type(val_utf8) # bytes

# Decoding bytes into characters.
val_utf8.decode('utf-8') # español 
```

## `string` module

### `string.ascii_lowercase`

- abc...z

## Rabin Karp

- A linear expected-time algorithm for string matching
- Based on hashing
- A good example of a randomized algorithm is if we pick $M$ in some random way

[Ref](https://www.youtube.com/watch?v=qQ8vS2btsxI&ab_channel=AbdulBari`)

## String matching

- Some auxiliary information must be maintained to mark the end of a string
  - a special end-of-string character OR
  - a count n of the characters in the string.
