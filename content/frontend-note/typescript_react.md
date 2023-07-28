---
title: Typescript and React
description: Typescript and React
summary: "Updated by Fatma, Jul 27, 2023."
date: 27-07-2023
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

## React `useState` hook with TypeScript

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
