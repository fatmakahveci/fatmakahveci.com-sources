---
title: Redux
description: Redux
summary: "Updated by Fatma, Sep 21, 2023."
date: 21-09-2023
categories:
  - "Coding"
tags:
  - "redux"
  - "coding"
  - "frontend"
  - "web development"
comments: true
---

![redux](/img/redux.png)

If you've dabbled in front-end web development, you've probably heard of Redux. It's a powerful state management library for JavaScript (JS) applications that has gained widespread popularity. In this post, I will provide an introduction.

## What is Redux?

Redux is a pattern and library for managing and updating application state, using events called "actions".

## Redux is useful when

- you have large amounts of application state needed in many places
- the app state is updated frequently
- updating the state can involve complex logic
- the app has a medium or large-sized codebase, and might be worked on by many people

## Redux Toolkit

- It is an approach for writing Redux logic.
- It contains packages and functions that are essential for building a Redux app.

## Store

- The current Redux application state lives in an object called the store.
- `Store` is created by passing in a reducer. It has `getState` method that returns the current state value.

## Actions

- An action is a plain JS object that has a `type` field.
- It is like an event that describes something that happened in the application.

## Reducers

- A reducer is a function that receives the current `state` and `action` objects, decides how to update the state if necessary, and returns the new state: `(state,action) => newState`.
- It must always follow the following rules:
  - It should only calculate the new state value based on the state and action arguments.
  - It is not allowed to modify the existing `state`. It must make immutable updates by copying the existing `state` and making changes to the copied values.
  - It must not do any asynchronous logic, calculate random values, or cause other "side effects".

## Dispatch

- `Store` has a `dispatch` method. Only calling `store.dispatch()` updates the state and passes in an action object.
- Dispatching actions is like triggering an event.
