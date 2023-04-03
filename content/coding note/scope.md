---
title: Scope
description: Scope
summary: "Updated by Fatma, Mar 28, 2023."
date: 28-03-2023
categories:
  - "Coding"
tags:
  - "coding"
  - "algorithms"
  - "data structures"
---

- **Precedence:** Local-> Enclosed-> Global -> Built-in

## 1. Built-in scope

- This is the scope of all the keywords.
- This is the largest scope.
- These load when the interpreter starts and we can access them from any part.

## 2. Global scope

- This is the scope of the variables that are created outside the functions.
- These can be accessed from any part of the program.

## 3. Local scope

- This is the scope of the variables created inside the functions.
- These exist only while the function is executing.
- We cannot access them outside the function.

## 4. Enclosed or nonlocal scope

- This case occurs when we have nested functions.
- The variables in the outer function are neither global nor local to the inner function.
- These have nonlocal scope.