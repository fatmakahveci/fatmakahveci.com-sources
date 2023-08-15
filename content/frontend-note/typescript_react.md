---
title: Typescript and React
description: Typescript and React
summary: "Updated by Fatma, Aug 15, 2023."
date: 15-08-2023
categories:
  - "Coding"
tags:
  - "typescript"
  - "user interface"
  - "coding"
  - "framework"
  - "frontend"
  - "web development"
  - "react"
comments: true
---

## 1. Hello, world

### 1.1 Create a React App

```bash
yarn create react-app <appName> --template typescript
```

### 1.2 Start the React App

```bash
yarn start
```

## 2. React hooks with TypeScript

### 2.1 `useState`

- `Typescript (TS)` can infer the type of certain variables based on initialisation if a lack of explicit information.

- If the state is immediately initialised upon declaration, you do not need to make any changes.

```typescript
const [count, setCount] = useState(0); // It infers that 0 is a number.
```

- `null`, `undefined` or some object with incomplete data type cause an error.

```typescript
const [state, setState] = useState(); // error
const [state, setState] = useState(null); // error

const [state, setState] = useState({
    state: '', // if secondState defined in setState({ state: '', secondState: ''});
})
```

```typescript
type User = {
  email: string;
  username?: string;
}; // Now it works.

const [user, setUser] = useState<User>({
    email: "",
});

// Array
const [users, setUsers] = useState<User[]>([]);
// OR
const [users, setUsers] = useState<Array<User>>([]); 
```

### 2.2 `useEffect`

- `TS` will not allow you to return anything other than _a function_ or `undefined` for `useEffect`.

### 2.3 `useReducer`

- `TS` will infer the return type of reducer if you do not define it.

### 2.4 `useRef`

- In `TS`, `useRef` returns a reference that is either `readonly` or `mutable`. It depends on whether your type argument fully covers the initial value or not.
  - **To access a DOM element:** provide only the element type as argument, and use `null` as initial value. It will return `readonly`.
  - **To have a mutable value:** provide the type you want, and make sure the initial value fully belongs to that type.

### 2.5 `useCallback`

- `TS` knows that `useCallback` accepts a function and an array of dependencies.

## 3. `React.ReactNode`

- A `ReactNode` is one of the following types:
  - `boolean`
  - `null` or `undefined`
  - `number`
  - `string`
  - A React element (result of JSX)
  - An array of any of the above, possibly a nested one.

## 4. `children` parameter

- It describes what child elements have, if any.
- A child element could be any ReactNode.
