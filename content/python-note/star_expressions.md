---
title: Star expressions
description: Star expressions
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
- They are useful when iterating over a sequence of tuples of varying lengths.

- Also, they are useful when combined with certain kinds of string processing operations, such as splitting.

  ```python
  line = 'nobody:*:-2:-2:Unprivileged User:/var/empty:/usr/bin/false'
  
  uname, *fields, homedir, sh = line.split(':')
  ```

- Examples

  - You want to drop the first and last grades and return the average of the remaining grades:

    ```python
    def drop_first_last(grades):
      first, *middle, last = grades
      return avg(middle)
    ```

  - You have a single name and email, but an arbitrary number of phone numbers.

    ```python
    name, email, *phone_numbers = ('Dave', 'dave@example.com', '2312', '32121')
    # phone_numbers = ['2312', '32121']
    ```

    Here `phone_numbers` will be always a list, regardless of the number of numbers including `None`.

  - ```python
    name, *_, (*_, year) = ('ACME', 50, 123.45, (12, 18, 2012))
    # name = 'ACME', year=2012
    ```
