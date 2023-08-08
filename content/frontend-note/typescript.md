---
title: Typescript
description: Typescript
summary: "Updated by Fatma, Jul 28, 2023."
date: 28-07-2023
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

## 1. Installation

### 1.1 `Node.js` and `npm` (node package manager)

- They are required to setup the environment. After installing them, you can check using the following commands:

  ```bash
  node -v # checks the version
  npm -v # checks the version
  ```

### 1.2 `typeScript`

```bash
npm install -g typescript
```

- The line above installs the `TypeScript` Compiler `tsc` globally.
- You can also use `npx` to run `tsc` from a local `node_modules` package instead.

## 2. Hello world

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

## 3. Compilation

- Because browsers and `Node.js` process only `JavaScript`, you must compile your `TypeScript` code before running or debugging it.
  - `tsc <file1>.ts <file2>.ts --outDir ./dist` keeps the directory clean.

## 4. Data types

### 4.1 Primitive types

#### 4.1.1 `string`

```typescript
var greeting: string = "Hello World";
console.log(greeting.toLowerCase()); // "hello world"
console.log(greeting); // "Hello World"

// Multi-line strings
let firstName: string = `Bob`;
let profile: string = `Hello
I'm ${firstName}.`;
```

#### 4.1.2 `number`

- There's no equivalent to `int` or `float`, but big integers get the type `bigint`.

```typescript
// Binary numbers := 0b... or 0B...
let bin = 0b100;
let anotherBin: number = 0B010;

// Octal numbers := 0o...
let octal: number = 0o10;

// Hexadecimal numbers := 0x... or 0X...
// The digits after the 0x must be in the range (0123456789ABCDEF).
let hexadecimal: number = 0XA;

// Big integers := ...n
let big: bigint = 9007199254740991n;
```

#### 4.1.3 `boolean`

- `true` and `false`

### 4.2 `array`

```typescript
// let arrayName: type[];

let list: number[] = [1, 2, 3];
let list: Array<number> = [1, 2, 3];
```

- `forEach()`, `map()`, `reduce()`, and `filter()` are useful array methods.

```typescript
let arr: number[] = [1, 2]; // [ 1, 2 ]
let square: number[] = arr.map(e => e * e); // [ 1, 4 ]
```

- Mixed types

```typescript
let scores : (string | number)[];
scores = ['Bob', 100]; // [ 'Bob', 100 ]
```

### 4.3 `any`

- You can use whenever you don't want a particular value to cause typechecking errors, except instead of `never`.

```typescript
let looselyTyped: any = 4;
looselyTyped.ifItExists(); // OK, ifItExists might exist at runtime
looselyTyped.toFixed(); // OK, toFixed exists (but the compiler doesn't check)

let strictlyTyped: unknown = 4;
strictlyTyped.toFixed();
```

### 4.4 `never`

- It indicates that a function will never return or that a value will never be assignable to a particular type. Typically, it represents the return type of a function that always throws an error.

```typescript
function raiseError(message: string): never {
    throw new Error(message);
}
```

### 4.5 Type annotations on variables

#### 4.5.1 `var`

- `var` is valid.
- `var name: string = 'Simon';`

#### 4.5.2 `let`

- `let` creates a variable.
- It allows you to declare block-level variables.
- The declared variable is available from the block it is enclosed in.

```typescript
let name: string = 'Simon';
```

#### 4.5.3 `const`

- `const` creates a constant value. (mostly)
- `const` variables are never intended to change.

```typescript
const Pi: number = 3.14;
```

### 4.6 Composing types

#### 4.6.1 Union (`|`)

- It declares that an object can be more than one type.
  - `type StringOrNumber = string | number;`

### 4.7 `Date`

```typescript
function greet(person: string, date: Date) {
    console.log(`Hello ${person}, today is ${date.toString()}`);
}
greet("Bob", new Date(2023, 5, 28));
```

### 4.8 `enum`

- You can define a set of named constants using `enum`.

```typescript
enum Color {
  Red = 1,
  Green = 2,
  Blue = 4,
}
let c: Color = Color.Green;
```

### 4.9 `object`

- It represents the non-primitive type.
- It refers to any JavaScript value with properties.
- To define an object type, we simply list its properties and their types.
- Object types are functions, arrays, classes, etc.

```typescript
function printCoord(pt: { x: number; y: number }) { }

// combined representation
let employee: {
    firstName: string;
    lastName: string;
} = {
    firstName: 'Jane',
    lastName: 'Doe',
};

// empty
let vacant: {} = {};
```

#### 4.9.1 Optional properties

- When you read from an optional property, you must check for `undefined` before using it.

```typescript
function printName(obj: { first: string; last?: string }) { }

printName({ first: "Bob" });
printName({ first: "Alice", last: "Alisson" });
```

#### 4.9.2 Readonly properties

- A readonly property should be modifiable only when the object first created.

```typescript
interface Person {
    readonly ssn: string;
    name: string;
}

let person: Person;
person = {
    ssn: '171-28-0926',
    name: 'Bob'
}
```

### 4.10 `null` and `undefined`

- These primitive values are used to signal absent or uninitialized value.

```typescript
let u: undefined = undefined;
let n: null = null;
```

### 4.11 `tuple`

```typescript
const passingResponse: [string, number] = ["{}", 200]; // [ '{}', 200 ]
let colour: [number, number, number] = [255, 0, 0]; // [ 255, 0, 0 ]
```

```typescript
type PayStubs = [StaffAccount, ...number[]];
const payStubs: PayStubs[] = [
  [staff[0], 250],
  [staff[1], 250, 260],
  [staff[0], 300, 300, 300],
];
```

### 4.12 `unknown`

- It describes the type of variables that we do not know when we are writing the code.

```typescript
let notSure: unknown = 4; // OK
notSure = "maybe a string instead"; // OK
notSure = false; // OK
```

### 4.13 `void`

- It is a little like the opposite of any: the absence of having any type at all. It is a good practice to add the void type as the return type of a function or a method that doesn't return any value.

```typescript
function warnUser(): void {
  console.log("This is my warning message");
}
```

### 4.14 `bigint`

- For very large integers.

```typescript
const oneHundred: bigint = BigInt(100);
const anotherHundred: bigint = 100n;
```

### 4.15 `symbol`

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

## 5. Functions

- Declaring a function:

```typescript
let sayHi: (name: string) => string;

sayHi = function (name) {
    return `Hi ${name}!`;
};

console.log(sayHi('Bob')); // Hi Bob!
```

### 5.1 Parameter type annotations

```typescript
function greet(name: string) {
  console.log("Hello " + name.toUpperCase());
}
```

### 5.2 Return type annotations

```typescript
function getNumber(): number {
  return 1;
}
```

### 5.3 Anonymous functions

```typescript
const names = ["Alice", "Bob", "Eve"];
 
names.forEach(function (s) {
  console.log(s.toUpperCase());
});
 
names.forEach((s) => {
  console.log(s.toUpperCase());
});
```

## 6. Interfaces and type aliases

- The key distinction is that a `type` cannot be re-opened to add new properties vs an `interface` which is always extendable.
- Interfaces define contracts and provide explicit names for type checking.
- Interfaces may have optional properties or readonly properties.
- Interfaces can be used as function types.

### 6.1 Interfaces

```typescript
interface Point {
  x: number;
  y: number;
}

function printCoord(pt: Point) { }

interface ThisPoint extends Point { }
```

- An interface can extend one or multiple interfaces or a class.

```typescript
interface <InterfaceX> {
  x(): void
}

interface <InterfaceY> {
  y(): void
}

interface <InterfaceZ> extends <InterfaceX>, <InterfaceY> {
  z(): string
}
```

- Only the class itself or its subclasses are allowed to implement the interface, if a class contains private or protected members.

```typescript
class Cat {
  private _age: number = 0;
}

interface StrayCat extends Cat {
  play(): void
}

class YellowStrayCat extends Cat implements StrayCat {
  play() {
    console.log('I like toys.')
  }
}

const yellowStrayCat = new YellowStrayCat();
yellowStrayCat.play();
```

### 6.2 Type aliases

- A type alias is exactly that - a name for any type.

```typescript
type Point = {
  x: number;
  y: number;
};

function printCoord(pt: Point) { }

// intersection

type <bothType> = <firstType> & <secondType>; // <bothType> will have all properties from both the first and second.

// union
type alphanumeric = string | number; // Alphanumerics holds a value of either string or number.

let input: alphanumeric;
input = 'Bob'; // valid
input = 1900; // valid
```

#### 6.2.1 String literal type

```typescript
type MouseEvent: 'click' | 'dblclick' | 'mouseup' | 'mousedown';
let mouseEvent: MouseEvent;
mouseEvent = 'click'; // valid
mouseEvent = 'dblclick'; // valid
```

#### 6.2.2 Type casting

```typescript
let a: typeA;
let b = <typeB>a;
```

## 7. Type assertions

- They are removed by the compiler, like a type annotation, and won't affect the runtime behavior of your code.

```typescript
const myCanvas = document.getElementById("main_canvas") as HTMLCanvasElement;

const myCanvas = <HTMLCanvasElement>document.getElementById("main_canvas"); // you can use <>, except if the code is in a .tsx file
```

## 8. Literal types

```typescript
// combining literal types (return)
function compare(a: string, b: string): -1 | 0 | 1 {
  return a === b ? 0 : a > b ? 1 : -1;
}
```

## 9. Narrowing

- The process of refining types to more specific types than declared is called narrowing.

```typescript
function padLeft(padding: number | string, input: string) {
  if (typeof padding === "number") {
    return " ".repeat(padding) + input; // padding:= number
  }
  return padding + input; // padding:= string
}
```

## 10. `typeof`

- It shows the type of values we have at runtime.

## 11. Type predicate

- To define a user-defined type guard, we simply need to define a function whose return type is a type predicate:

```typescript
let pet = getSmallPet();

if (isFish(pet)) {
  pet.swim();
} else {
  pet.fly();
}
```

## 12. Parameters

### 12.1 Rest parameters

- It allows you to represent an indefinite number (zero or more) of arguments as an array.

```typescript
function <function_name>(...<parameter_name>: <parameter_type>[]) { }
```

- Rules:
  - A function has only one rest parameter.
  - The rest parameter appears last in the parameter list.
  - The type of the rest parameter is _array_.

### 12.2 Default parameters

- The default initialised value for the _omitted_ parameters.
- Default parameters don't need to appear after the required parameters. When a default parameter appears before a required parameter, you need to explicitly pass `undefined` to get the default initialised value.

```typescript
function <function_name>(<parameter_name>: <parameter_type>=<default_value>,...): <return_type_if_any>{ }
```

### 12.3 Optional parameters

- Optional parameters must come after the required parameters.
- Using `?` after the parameter name makes a function parameter optional.

```typescript
function <function_name>(<parameter_name>?: <parameter_type>=<default_value>,...): <return_type_if_any>{ }
```

## 13. Class

```typescript
class Cat {
    catName: string;

    constructor(catName: string) {
        this.catName = catName;
    }

    getCatName(): string {
        return `${this.catName}`;
    }
}

let cat = new Cat('Puffy');
```

### 13.1 Getters and setters

```typescript
class Cat {
  private _age: number = 0;

  public get age(): number {
    return this._age;
  }

  public set age(newAge: number) {
    if (newAge < 0) {
      throw new Error('Age is invalid.');
    }
    else if (newAge > 1) {
        console.log('Not a kitten');
    }
    this._age = newAge;
  }
}

const cat = new Cat();
console.log(cat); // 0

cat.age = 5; // Not a kitten
console.log(cat); // 5

cat.age = -1; // Age is invalid.
```

## 14. Static methods and properties

- A static property is shared among all instances of a class.

```typescript
class Cat {
  static counter: number = 0;

  constructor(private catName: string) {
    Cat.counter++;
  }
    
  public static getCounter() {
    return Cat.counter;
  }
}

let simba = new Cat('Simba');
let felix = new Cat('Felix');

console.log(Cat.counter); // 2
console.log(Cat.getCounter()); // 2
```

## 15. Abstract class

- It defines common behaviours for derived classes to extend.
- Unlike a regular class, it cannot be instantiated directly.
- To use it, you must inherit and implement its abstract methods.
- It often contains one or more abstract methods.

```typescript
abstract class Cat {
  constructor(private catName: string) { }

  abstract getSpecies(): string 
}

class SpecificCat extends Cat {
  constructor(catName: string, private species: string) {
    super(catName);
  }

  getSpecies(): string {
    return this.species;
  }
}

let simba = new SpecificCat('Simba', 'stray cat');

console.log(simba.getSpecies()); // stray cat
```

## 16. Operators

### 16.1 Non-null assertion operator `!`

- `!` says that it will never be `null` or `undefined`.

```typescript
interface Person {
    name: string
    age: number
}

function printName(person?: Person) {
  // If we don't put an exclamation mark (person!) an error will
  // occur, 'person' is possibly 'undefined'.
    console.log(`The name is ${person!.name}`)
}
```

### 16.2 Nullish coalescing operator `??`

- `??` returns the first argument if it's not `null`/`undefined`. Otherwise, the second one.

```typescript
a ?? b // equals to
( a!== null && a!== undefined ) ? a : b
```

### 16.3 `in`

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

### 16.4 `instanceof`

- It has an operator for checking whether or not a value is an “instance” of another value.
