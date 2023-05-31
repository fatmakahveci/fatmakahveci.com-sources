---
title: The programmers brain
description: Some of the influential parts from the books that I have read.
summary: "Updated by Fatma, May 05, 2023."
date: 05-05-2023
categories:
  - "blog_posts"
tags:
  - "post"
  - "reading"
comments: true
---
## [The programmers brain](https://www.manning.com/books/the-programmers-brain)

### 1 Cognitive processes in programming

- Confusion is acceptable for a while when you start to work in a new domain. Not knowing the meaning of a concept and trying to read complex code are distinct ways of confusion. Each relates to a different cognitive process.
- Three ways of confusion:
  - __A lack of knowledge:=__ issue in long-term memory (LTM)
    - e.g., not knowing the meaning of an operator.
    - The relevant facts are insufficient in your LTM.
  - __Lack of information:=__ issue in short-term memory (STM)
    - e.g., not knowing the inner workings of a function.
    - STM stores information temporarily.
  - __Lack of processing power:=__ issue in working memory
    - You cannot process the entire execution despite an educated guess.

![memory.png](/img/memory.png)

- Three cognitive processes:
  - __Long-term memory:=__ a computer's hard drive
    - LTM is involved in everything we do.
    - e.g., writing binary search requires you to remember
      - the abstract algorithm
      - the syntax of the programming language (PL)
      - how to type on a keyboard
  - __Short_term memory:__ a computer's RAM or cache
    - e.g., keywords, variable names, and data structures when reading a program.
    - The estimated size of an STM is not more than a dozen of items.
    - STM is emptied when you solve the problem.
  - __Working memory:__ a computer's processor
    - You do tracing and other cognitively complex tasks here.
      - _Tracing_ is the mental compiling and executing of code.
    - You form new thoughts, ideas, and solutions here.

### 2 Read code quickly and get a sense of its workings

- STM and LTM
  - Information passes through sensory memory before it reaches STM.
    - Each of the five senses has its cache in the sensory memory.
    - _iconic memory_ is for the sense of sight
      - You can remember more information about code than you can process in your STM. _Code at a glance_ exercise will help you gain an initial image of the code.
        - Look at the code for a few seconds, then remove it from sight and try to answer the following questions:
          - What is the structure of the code?
            - Is the code nested deeply, or is it flat?
            - Are there any lines that stand out?
          - How is whitespace used to structure the code?
            - Are there gaps in the code?
            - Are there large blobs of code?
  - STM first stores information when you read code.
    - The time and size (2-6 things) limit STM to remember the information.
      - STM and LTM collaborate to overcome STM's size limitation.
  - LTM
    - syntactic knowledge of PL
    - know the algorithm before
  - Lack of practice makes code reading harder.

- Code reading
  - We often read code to
    - add a feature
      - the right location to implement
    - find a bug, and
      - the location of a specific bug where you last edited the code
      - how a certain method is implemented
    - build an understanding of a large system.

- Chunking
  - When you read new information, your brain tries to divide the information into recognizable parts called chunks.
  - If you want to write code that is easy to chunk, make use of design patterns.
  - To deliberately practice chunking, actively try to remember code. Ask yourself:
    - Which parts did you produce correctly with ease?
    - Are there any parts of the code that you reproduced partly?
    - Are there parts of the code that you missed entirely?
    - Do you understand why you missed the lines that you did?
    - Do the lines of code that you missed contain programming concepts that are unfamiliar to you?
    - Do the lines of code that you missed contain domain concepts that are unfamiliar to you?

- Comments
  - Add comments for your junior developers. Beginners focus more on comments.

- Beacons
  - They are parts of a program that help a programmer understand what the code does.
    - _Simple beacons_ are self-explaining syntactic code elements, such as meaningful variable names.
    - _Compound beacons_ do not offer much insight into the code, but together they do. For instance, a for-loop can be a compound beacon because it contains the variable, the initial assignment, and the increment and the boundary values.
  - Ask yourself:
    - What beacons have you collected?
    - Are these code elements or natural language information?
    - What knowledge do they represent?
    - Do they represent knowledge about the domain of the code?
    - Do they represent knowledge about the functionality of the code?

### 3 Learn programming syntax and concepts

- The use of LTM, different forms of remembering, and ways to strengthen the cognitive process

### 4 Read complex code

- Information overload and how to prevent the brain from overloading

### 5 Understanding of unfamiliar code deeply

### 6 Solve programming problems better

### 7 Avoid bugs in code and in thinking

### 8 Select clear variable names

### 9 Code smells and the cognitive principles behind them

### 10 Advanced techniques to solve complex problems

### 11 The act of coding and variety of tasks in programming

### 12 Improve large code bases

### 13 Less painful onboarding process of new developers

---

Updated by _Fatma_ on April 05, 2023
