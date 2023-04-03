---
title: Regex
description: Regex
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
```python
import re

# r'':= means raw string, of which use is recommended.
# r'\t' := backslash
# '\t' := tab

re.findall(<pattern>, <text>)
re.split(<pattern>, <text>)
re.sub(<pattern>, <replace>, <text>)

match = re.search(<pattern>, <text>) # the first location else None
match.group() #returns the part of the string where there is a match
```

## re.compile()

- It compiles a regex pattern provided as a string into a regex pattern object (re.Pattern). Later we can use this pattern object to search for a match inside different target strings using regex methods such as a `re.match()` or `re.search()`.

```python
import re

regex_pattern = re.compile(r"\d{3}")
result = regex_pattern.findall("Emma's luck numbers are 251 761 231 451")
```

---

- Any character except the new line

## ^

- beginning of a string. i.e.,
  - ^a...s$ := alias, abyss, etc.

## $

- end of a string

## []

- matches characters in brackets. i.e.,
  - [abc] := a (1 match), ac (2 matches), abc de ca (5 matches), etc.
  - [a-e] := [abcde]
  - [1-4] := [1234]

## [^ ]

- matches characters not in brackets. i.e.,
  - [^abc]:= any character except a or b or c

## *

- 0 or more. i.e.,
  - ma\*n:= mn, man, main, etc.

## +

- 1 or more. i.e.,
  - ma+n:= man, main, etc.

## ?

- 0 or one. i.e.,
  - ma?n := man, mn, woman, etc.

## {<#>}

- exact number. i.e.,
  - a{2,3} := abc daat (1 match), aabc daat (2 matches), etc.

## {<#>,<#>}

- range of numbers (minimum, maximum). i.e.,
  - [0-9]{2,4} := matches at least 2 digits but not more than 4 digits:= 123 (123), 12 345673 (12 3456 78), etc.

## |

- or. i.e.,
  - a|b := ade (1 match), acdbea (a b a) (3 matches), etc.

## ()

- group subpatterns. i.e.,
  - (a|b|c)xz := ab axz cabxz (axz bxz) (2 matches), etc.

## \A

- matches if the specified characters are at the beginning. i.e.,
  - \Athe:= the sun, etc.

## \Z

- matches if the specified characters are at the end. i.e.,
  - Python\Z:= I like Python, etc.

## \b

- word boundary, matches if the specified characters are at the beginning or the end. i.e.,
  - \bfoo := football
  - foo\b := the foo

## \B

- not word boundary, matches if the specified characters are NOT at the beginning or the end. i.e.,
  - \Bfoo := a football, etc.
  - foo\B := the afootest, etc.

## \d

- digit. i.e.,
  - \d:= 12abc3 (1 2 3) (3 matches), etc.

## \D

- not a digit. i.e.,
  - \D := 1ab34"50 (a b ") (3 matches), etc.

## \s

- contains whitespace. i.e.,
  - \s:= a b ( ) (1 match), etc.

## \S

- not contain whitespace. i.e.,
  - \S:= a b (a b) (2 matches), etc.

## \w

- word. == [a-zA-Z0-9_] i.e.,
  - \w := 12&": ;c (1 2 c)(3 matches), etc.

## \W

- not word. i.e.,
  - \W:= 1a2%c (%) (1 match), etc.

```python
import re

text_to_search = '''
abcdefghijklmnopqrstuvwxyz
ABCDEFGHIJKLMNOPQRSTUVWXYZ
1234567890

Ha HaHa

MetaCharacters (Need to be escaped):
. ^ $ * ? { } [ ] \ | ( )

coreyms.com

321-555-4321
900-555-4321
800-555-4321
123.555.1234
123-.555.1234
123*555*1234

Mr. Schafer
Mr Smith
Ms Davis
Mrs. Robinson
Mr. T

cat
mat
pat
bat
'''

sentence = 'Start a sentence and then bring it to an end'

# one character [.-]
# pattern = re.compile(r'[89]00[-.]\d\d\d[-.]\d\d\d'))
# pattern = re.compile(r'\d\d\d[-.]\d\d\d[-.]\d\d\d')
# pattern = re.compile(r'[^b]at')

pattern = re.compiler(r'')

matches = pattern.finditer(text_to_search)

for match in matches:
 print(match)

##

import re

pattern = '^a...s$'
text = 'abyss'
result = re.match(pattern, text) # True

##
```
