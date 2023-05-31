---
title: Typescript
description: Typescript
summary: "Updated by Fatma, May 30, 2023."
date: 30-05-2023
categories:
  - "Coding"
tags:
  - "typescript"
  - "user interface"
  - "coding"
  - "framework"
  - "frontend"
  - "web development"
comments: true
---

![header](/img/typescript_header.png)

- `Typescript` offers all `JS`'s features, and typing system.
- It also supports object-oriented programming as `JS`.

## Installation

### `Node.js` and `npm` (node package manager)

- They are required to setup the environment. After installing them, you can check using the following commands:

  ```bash
  node -v # checks the version
  npm -v # checks the version
  ```

### `typeScript`

```bash
npm install -g typescript
```

- The line above installs the `TypeScript` Compiler `tsc` globally.
- You can also use `npx` to run `tsc` from a local `node_modules` package instead.

## Hello world

```typescript
// typeScript filename: greeting.ts
var greeting: string = "Hello World";
console.log(greeting);
```

```bash
# bash: compilation (ts -> js)
tsc greeting.ts

# bash: run javascript file
node greeting.js
```

## Compilation

- Because browsers and `Node.js` process only `JavaScript`, you must compile your `TypeScript` code before running or debugging it.
  - `tsc <file1>.ts <file2>.ts --outDir ./dist` keeps the directory clean.

## Data types

### Primitive types

#### `string`

```typescript
var greeting: string = "Hello World";
console.log(greeting.toLowerCase());
console.log(greeting);
```

#### `number`

- There's no equivalent to `int` or `float` - everything is simply `number`.

#### `boolean`

- `true` and `false`

### `array`

```typescript
let list: number[] = [1, 2, 3];
let list: Array<number> = [1, 2, 3];
```

### `any`

- You can use whenever you don't want a particular value to cause typechecking errors, except instead of `never`.

```typescript
let looselyTyped: any = 4;
looselyTyped.ifItExists(); // OK, ifItExists might exist at runtime
looselyTyped.toFixed(); // OK, toFixed exists (but the compiler doesn't check)

let strictlyTyped: unknown = 4;
strictlyTyped.toFixed();
```

### `never`

- It indicates that a function will never return or that a value will never be assignable to a particular type.

### Type annotations on variables

#### `var`

- `var` is valid.
- `var name: string = 'Simon';`

#### `let`

- `let` creates a variable.
- It allows you to declare block-level variables.
- The declared variable is available from the block it is enclosed in.

```typescript
let name: string = 'Simon';
```

#### `const`

- `const` creates a constant value. (mostly)
- `const` variables are never intended to change.

```typescript
const Pi: number = 3.14;
```

### Composing types

#### Union (`|`)

- It declares that an object can be more than one type.
  - `type StringOrNumber = string | number;`

### `Date`

```typescript
function greet(person: string, date: Date) {
    console.log(`Hello ${person}, today is ${date.toString()}`);
}
greet("Bob", new Date(2023, 5, 28));
```

### `enum`

- You can define a set of named constants using `enum`.

```typescript
enum Color {
  Red = 1,
  Green = 2,
  Blue = 4,
}
let c: Color = Color.Green;
```

### `object`

- It represents the non-primitive type.
- It refers to any JavaScript value with properties.
- To define an object type, we simply list its properties and their types.

```typescript
function printCoord(pt: { x: number; y: number }) {}
```

#### Optional properties

- When you read from an optional property, you must check for `undefined` before using it.

```typescript
function printName(obj: { first: string; last?: string }) {}

printName({ first: "Bob" });
printName({ first: "Alice", last: "Alisson" });
```

### `null` and `undefined`

- These primitive values are used to signal absent or uninitialized value.

```typescript
let u: undefined = undefined;
let n: null = null;
```

### `tuple`

```typescript
const passingResponse: [string, number] = ["{}", 200];
```

```typescript
type PayStubs = [StaffAccount, ...number[]];
const payStubs: PayStubs[] = [
  [staff[0], 250],
  [staff[1], 250, 260],
  [staff[0], 300, 300, 300],
];
```

### `unknown`

- It describes the type of variables that we do not know when we are writing the code.

```typescript
let notSure: unknown = 4; // OK
notSure = "maybe a string instead"; // OK
notSure = false; // OK
```

### `void`

- It is a little like the opposite of any: the absence of having any type at all. You may commonly see this as the return type of functions that do not return a value:

```typescript
function warnUser(): void {
  console.log("This is my warning message");
}
```

### `bigint`

- For very large integers.

```typescript
const oneHundred: bigint = BigInt(100);
const anotherHundred: bigint = 100n;
```

### `symbol`

- `symbol` := immutable and unique

```js
const value1 = Symbol('hello');
const value2 = Symbol('hello');
console.log(value1 === value2); // false
```

```js
// symbol
for()
keyFor()
toSource()
toString()
valueOf()
```

## Functions

### Parameter type annotations

```typescript
function greet(name: string) {
  console.log("Hello " + name.toUpperCase());
}
```

### Return type annotations

```typescript
function getNumber(): number {
  return 1;
}
```

### Anonymous functions

```typescript
const names = ["Alice", "Bob", "Eve"];
 
names.forEach(function (s) {
  console.log(s.toUpperCase());
});
 
names.forEach((s) => {
  console.log(s.toUpperCase());
});
```

## Interfaces and type aliases

- The key distinction is that a `type` cannot be re-opened to add new properties vs an `interface` which is always extendable.

### Interfaces

```typescript
interface Point {
  x: number;
  y: number;
}

function printCoord(pt: Point) {}
```

### Type aliases

- A type alias is exactly that - a name for any type.

```typescript
type Point = {
  x: number;
  y: number;
};

function printCoord(pt: Point) {}
```

## Type assertions

- They are removed by the compiler, like a type annotation, and won't affect the runtime behavior of your code.

```typescript
const myCanvas = document.getElementById("main_canvas") as HTMLCanvasElement;

const myCanvas = <HTMLCanvasElement>document.getElementById("main_canvas"); // you can use <>, except if the code is in a .tsx file
```

## Literal types

```typescript
// combining literal types (return)
function compare(a: string, b: string): -1 | 0 | 1 {
  return a === b ? 0 : a > b ? 1 : -1;
}
```

## Narrowing

- The process of refining types to more specific types than declared is called narrowing.

```typescript
function padLeft(padding: number | string, input: string) {
  if (typeof padding === "number") {
    return " ".repeat(padding) + input; // padding:= number
  }
  return padding + input; // padding:= string
}
```

### `in`

- `in` operator determines if an object has a property with a name.

```typescript
type Fish = { swim: () => void };
type Bird = { fly: () => void };

function move(animal: Fish | Bird) {
  if ("swim" in animal) {
    return animal.swim();
  }
  return animal.fly();
}
```

### `instanceof`

- It has an operator for checking whether or not a value is an “instance” of another value.

## `typeof`

- It shows the type of values we have at runtime.

## Type predicate

- To define a user-defined type guard, we simply need to define a function whose return type is a type predicate:

```typescript
let pet = getSmallPet();

if (isFish(pet)) {
  pet.swim();
} else {
  pet.fly();
}
```
