---
title: React
description: React
summary: "Updated by Fatma, May 25, 2023."
date: 25-05-2023
categories:
  - "Coding"
tags:
  - "react"
  - "user interface"
  - "coding"
  - "framework"
  - "frontend"
  - "web development"
comments: true
---

![react](/img/react.gif)

- [React](`https://reactjs.org/docs/getting-started.html`) is a `Javascripty` library for building interactive user interfaces.

## The fundamentals of React

### 1. Component

- React composes complex UIs from small and isolated pieces of code called _components_.
- We use components to tell React what we want to see on the screen. When our data changes, React will efficiently update and re-render our components.
- A component is written as either a `.JSX` or `.JS` file. It is simply a JS class or function that returns some HTML code.
- A component file contains both logic and view written in `JS` and `HTML`, respectively.
- A component name and file name is always written in `TitleCase`.
- Imports are made at the top of a React component.
- React components are imported into other React components before using them.
- Using a component is as simple as declaring it inside of tags, for example: `<HelloWorld />`
- A component takes in parameters, called props and returns a hierarchy of views to display via the render method.
- The render method returns a description of what you want to see on the screen. React takes the description and displays the result. In particular, render returns a React element, which is a lightweight description of what to render.

- All React component classes that have a constructor should start with a super (props) call:

```javascript
class <className> extends React.Component {
  constructor(props) {
    super(props);
    // ...
  }
}
```

#### Server and client components

![component](/img/component.png)

- [Ref](https://nextjs.org/docs/getting-started/react-essentials#server-components)

### 2. Props

- React components use `props` to communicate with each other.
  - Every parent component can pass some information to its child components by giving them props.
  - You can pass any JS value through them, including objects, arrays, and functions.

#### Passing props to a component

```javascript
import { getImageUrl } from './utils.js';

function Photo(props) {
  let person = props.person;
  let size = props.size;

  return (
    <img
      className="photo"
      src={getImageUrl(person)}
      alt={person.name}
      width={size}
      height={size}
    />
  );
}

// Step 1: Pass props to the child component
export default function Profile() {
  return (
    <Photo
      person={{
        name: 'Bob Alice',
        imageId: '12ab'
      }}
      size={100}
    />
  );
}

// Step 2: Read props inside the child component
function Photo({ person, size = 50 }) {
  // variables are available here
}
```

- **[Prop drilling] (threading)** refers to the process you have to go through to get data to parts of the React component tree.
- It may cause problems while your project is growing. Below are some cases:
  - Refactoring the data: `{user: {name: 'Bob'}}` => `{user: {name: 'Bob', age: 70}}`
  - Passing redundant props or missing props due to moving a component
  - Renaming props makes tracking difficult for your brain

### 3. State

- All the React components can have a state associated with them.
- A state can change either due to
  - a response to an action performed by the user OR
  - en event triggered by the system.
- Whenever the state changes, React re-renders the component to the browser.

- The following lets you use local state within a function component.

```javascript
const [<currentState>, <functionToUpdateTheState>] = useState(`<initialState>`);
```

#### `setState`

- After building an initial state setup, we use `setState()` method to change the state object.

```javascript
setState({ stateName : updatedStateValue })
// OR
setState((prevState) => ({ 
  stateName: prevState.stateName + 1 
}))
```

---

## `package.json`

- One of the most important files is `package.json` which is React app's configuration file.
- It is central to provide any metadata about the project, add any additional libraries to our project, and configuring things like run scripts.

---

## `fontawesome`

- `fontawesome` will provide svgs as react components.

```bash
# installation
npm i --save @fortawesome/react-fontawesome @fortawesome/free-solid-svg-icons @fortawesome/fontawesome-svg-core
```

---

## JSX

- You can put any JS expressions within braces inside `JSX`.

```javascript
const element = <h1>Hello, world!</h1>;
const element = (
  <div>
    <h1>Hello!</h1>
  </div>
);
```

---

## Hooks

- `Hooks` let you use state and other React features without writing a class. They don't work inside classes.
- They let you hook into React state and lifecycle features from function components.
- Hooks are JS functions imposing two additional rules:
  
  1. Only call Hooks at the top level. Don't call Hooks inside loops, conditions, or nested functions.
  
  2. Only call Hooks from React function components. Don't call Hooks from regular JavaScript functions.

### 1. `useState` hook

`const [<currentState>, <functionToUpdateTheState>] = useState(<initialState>);` lets you use local state within a function component.

```javascript
import React, { useState } from 'react';

function Example() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

### 2. `useReducer` hook

- It is an alternative to `useState`. It is preferable to `useState` when you have complex state logic that involves multiple subvalues or when the next state depends on the previous one.

```javascript
const [state, dispatch] = useReducer(reducer, initialArg, init);

// specifying the initial state
// pass the initial state as a second argument
const [state, dispatch] = useReducer(
  reducer,
  {count: initialCount}
);
```

### 3. `useEffect` hook

- Fetching, subscriptions, or manually changing the DOM called "side effects (effects)" because they can affect other components and can't be done during rendering.
- Runs on every update

```javascript
import { useEffect } from 'react';

function <ComponentName> {
  useEffect(() => {});
}
```

- Runs ONCE after the initial rendering

```javascript
import { useEffect } from 'react';

function <ComponentName> {
  useEffect(() => {
  },[]);
}
```

- Runs if any dependency changes

```javascript
import { useEffect } from 'react';

function <ComponentName> {
  useEffect(() => {
  },[Dependencies]);
}
```

- Runs on cleanup

```javascript
import { useEffect } from 'react';

function <ComponentName> {
  useEffect(() => {
    return()=>{}
  },[]);
}
```

- Calling `useEffect` runs the "effect" function after flushing the changes to the DOM.
  - Effects are declared inside the component so they have access to its props and state.
  - By default, React runs the effects after every render, including the first.
- Just like `useState`, you can use multiple single effect in a component.

### 4. `useContext` hook

- React [context](https://reactjs.org/docs/context.html) is an interface for sharing information with other components without explicitly passing the data as `props`.
- It is flexible enough to use as a centralized state management system for the project, or you can scope it to smaller sections of your application.
- You can hold inside the context:
  - global state
  - theme
  - application configuration
  - authenticated user
  - user settings
  - prefferred language
  - a collection of services

#### 4.1. Create the context

- It creates a context instance.

```javascript
import { createContext from 'react' };

const Context = createContext('Default Value');
```

#### 4.2. Provide the context

- It provides the context to its child components, no matter how deep they are.

```javascript
function Main() {
  const value = 'My Context Value'; // update it to change the context value

  // <MyComponent /> to add the component
  return (
    <Context.Provider value={value}>
      <MyComponent />
    </Context.Provider>
  );
}
```

#### 4.3. Consume the context

- You can have multiple consumers for a single context. All customers will be notified and re-rendered depending on the context value change.

```javascript
import { useContext } from 'react';

function MyComponent() {
  const value = useContext(Context);

  return <span>{value}</span>;
}
```

OR

```javascript
function MyComponent() {
  return (
    <Context.Consumer>
      {value => <span>{value}</span>}
    </Context.Consumer>
  );
}
```

### 5. `useMemo` hook

- `const <cachedValue> = useMemo(<calculateValue>, [<dependencies>])` caches the result of a calculation between re-renders.
- It takes two arguments which are dependencies and a function that computes the value you want to memoize.
- It memoizes a value.
- It can avoid unnecessary recomputing.
- [Example code](https://www.youtube.com/watch?v=THL1OPn72vo)

### 6. `useCallback` hook

- `const <cachedFunctionName> = useCallback(<functionName>, [<dependencies>])` caches a function definition between re-renders.
- It takes two arguments which are dependencies and a function that you want to memoize.
- It memoizes a function.
- It can avoid re-rendering the child component every time the parent component is rendered.
- [Example code](https://www.youtube.com/watch?v=_AyFP5s69N4)

### 7. `useRef` hook

- `const <ref> = useRef(<initialValue>)` creates a reference value that's not needed for rendering.
  - **Parameter:** `<initialValue>` can be a value of any type.
  - **Return:** `<current>` is set to the `<initialValue>` initially, you can later change it.

- Changing a ref doesn't trigger a re-render so refs are ideal for storing information that doesn't affect the visual output of your component.

- **Example:** Focusing a text input

```js
import { useRef } from 'react';

export default function Form() {
  const inputRef = useRef(null);

  function handleClick() {
    inputRef.current.focus();
  }

  return (
    <>
      <input ref={inputRef} />
      <button onClick={handleClick}>
        Focus the input
      </button>
    </>
  );
}
```

### 8. `useImperativeHandle` hook

- `useImperativeHandle(<ref>, <createHandle>, [<dependencies>])` exposes a value, state or function inside a child component to the parent component through `ref`.
  - `<ref>` := ref passed down from the parent component
  - `<createHandle>`:= value to be exposed to the parent component
- You can decide which properties the parent component can access so you can maintain the private scoping of the child component.
- It is useful when you need bidirectional data.
- [Example code](https://www.youtube.com/watch?v=zpEyAOkytkU&list=PLZlA0Gpn_vH8EtggFGERCwMY5u5hOjf-h&index=12)

### 9. `useLayoutEffect` hook

- `useLayoutEffect(<setup>, [<dependencies>])` performs side effects.
  - `<setup>` := function containing the side effect logic
- It is a version of `useEffect` that fires before the browser repaints the screen. The main difference is the timing of when they are executed.
- It is useful when measuring the layout before the browser repaints the screen.

### 10. `useDebugValue` hook

- `useDebugValue(<value>, <format>)` adds a label to a custom hook.
  - `<value>` := any value that you want to display
  - `<format>` := an optional formatting function
- It is also useful when deferring the formatting of a debug value.

### 11. `useDeferredValue` hook

- `useDeferredValue(<value>)` defers updating a part of the UI.
  - `<value>` := any value that you want to defer
- It is also useful when showing stale content while fresh content is loading.

### 12. `useTransition` hook

- `const [<isPending>, <startTransition>] = useTransition()` updates the state without blocking the UI.
  - `<isPending>` flag that tells you whether there is a pending transition.
  - `<startTransition>` function that lets you mark a state update as a transition.
- It is useful when marking a state update as a non-blocking transition.

### 13. `useId` hook

- `const <id> = useId()` generates unique IDs that can be passed to accessibility attributes.

### 14. `useSyncExternalStore`

- `const <snapshot> = useSyncExternalStore(<subscribe>, <getSnapshot>, <getServerSnapshot>)` subscribes to an external store.
  - `<snapshot>`:= function that takes a single callback argument and subscribes it to the store
  - `<getSnapshot>`:= function that returns a snapshot of the data in the store that’s needed by the component
- It is useful when subscribing to an external store or a browser API, extracting the logic to a custom Hook, or adding support for server rendering.

### 15. `useInsertionEffect`

- `useInsertionEffect(<setup>, [<dependencies>])` is a version of `useEffect` that fires before any DOM mutations.
  - `<setup>` := function with your Effect's logic.
- It is useful when injecting dynamic styles from CSS-in-JS libraries.

---

## axios requests

- `axios` is a popular data fetching package on `npm`.
- It is an open-source and promise-based HTTP client.

```bash
npm install axios
```

### With `async/await`

- `async` is a function that pauses until the promise is resolved due to `await`. To pull out the response from the promise object, we use then and catch methods.
- `await` is an operator that is declared with the promise function. It is always defined inside the `async` function. It holds the execution of the promise function as long as the promise is completely fulfilled.

```javascript
import axios from "axios";

// GET
const getData = async () => {
  const response = await axios.get("<url>");
};

// POST
try {
  const url = "<url>";
  const data = {key: 'value'};
  const config = {'content-type': 'application/json'};

  const response = await axios.post(url, data, config);
  // <command>
} catch (error) {
  // <command>
}

// PUT
axios.put()

// DELETE
axios.delete()
```

---

## Handling events

- They are named using _camelCase_.
- With JSX you pass a function as the event handler.
- You cannot return `false` to prevent default behaviour in React. You must call `preventDefault` explicitly.

- Generally, if you refer to a method without `()`, you should bind that method.

```javascript
class Toggle extends React.Component {
  constructor(props) {
    super(props);
    this.state = {isToggleOn: true};

    // This binding is necessary to make `this` work in the callback
    this.handleClick = this.handleClick.bind(this);
  }

  handleClick() {
    this.setState(prevState => ({
      isToggleOn: !prevState.isToggleOn
    }));
  }
  
  render() {
    return (
      <button onClick={this.handleClick}>
        {this.state.isToggleOn ? 'ON' : 'OFF'}
      </button>
    );
  }
}
```

### Passing arguments to event handlers

- With an arrow function, we have to pass the React event `e` explicitly.

```javascript
<button onClick={(e) => this.deleteRow(id, e)}>Delete Row</button>
```

---

## Conditional rendering

```javascript
function UserGreeting(props) {
  return <h1>Welcome back!</h1>;
}

function GuestGreeting(props) {
  return <h1>Please sign up.</h1>;
}

function Greeting(props) {
  const isLoggedIn = props.isLoggedIn;

  if (isLoggedIn) {
    return <UserGreeting />;
  }
  return <GuestGreeting />;
}

const root = ReactDOM.createRoot(document.getElementById('root')); 

root.render(<Greeting isLoggedIn={false} />);
```

---

## match

- A `match` object contains information about how a `<Route path>` matched the URL.
  - `params` are key/value pairs from the URL corresponding to the dynamic segments of the path.
  - `isExact` is `true` if the entire URL was matched.
  - `path` is the pattern used to match.
  - `url` is the matched part of the URL.

---

## Lists and keys

```javascript
function ListItem(props) {
  return <li>{props.value}</li>;
}

function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    <ListItem key={number.toString()}
              value={number} />
  );
  return (
    <ul>
      {listItems}
    </ul>
  );
}

const root = ReactDOM.createRoot(document.getElementById('root'));
const numbers = [1, 2];
root.render(<NumberList numbers={numbers} />);
```

---

### Rendering Elements

- Rendering converts the code you write into user interfaces (UIs).
- An element is the smallest building block of React apps. It describes what you want to see on the screen.
- Each _React element_ is a JS object that you can store in a variable or pass around in your program.
- The only way to update the UI is to create a new element, and pass it to `root.render()`.

```js
const root = ReactDOM.createRoot(
  document.getElementById('root')
);

function tick() {
  const element = (
    <div>
      <h1>Hello world</h1>;
      <h2>It is {new Date().toLocaleTimeString()}.</h2>
    </div>
  );
  root.render(element);
}

setInterval(tick, 1000);
```

#### `setInterval`

- `setInterval` executes a function at specific intervals. It helps in checking a condition regularly or fetching data every so often.
- `clearInterval(<intervalName>)` stops the interval.

## Layouts

- A layout is UI that is shared between multiple pages.
