---
title: Typescript
description: Typescript
summary: "Updated by Fatma, Aug 09, 2023."
date: 09-08-2023
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
- Also, you can use `npx` to run `tsc` from a local `node_modules` package instead.

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

### 4.2 `Array`

```typescript
// let arrayName: type[];

let list: number[] = [1, 2, 3];
let list: Array<number> = [1, 2, 3];
```

- Mixed types

```typescript
let scores : (string | number)[];
scores = ['Bob', 100]; // [ 'Bob', 100 ]
```

- `Array.forEach()`, `Array.map()`, `Array.reduce()`, and `Array.filter()` are useful array methods.

#### 4.2.1 `Array.forEach()`

- It calls a function for each element in the array.

```typescript
let num = [1, 2, 3];
num.forEach(function (value) {
  console.log(value); // 1 2 3
});
```

#### 4.2.2 `Array.map()`

```typescript
let arr: number[] = [1, 2, 3];
let square: number[] = arr.map(e => e * e);
console.log(square); // [ 1, 4, 9 ]
```

#### 4.2.3 `Array.reduce()`

- It applies a function against two array values to reduce it to a single value.

```typescript
let arr: number[] = [1, 2, 3];
let val = arr.reduce(function(a, b) { // (a,b):= (previous, current)
  return a + b;
})
console.log(val); // 6
```

#### 4.2.4 `Array.filter()`

- It creates a new array with all elements that pass the test implemented by the provided function.

```typescript
function isEven(n: number) {
  if(n % 2 == 0) {
    return true;
  } else {
    return false;
  }
}

console.log([1, 2, 3].filter(isEven)); // [ 2 ]
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

- It indicates that a function will never return or a value will never be assignable to a particular type. Typically, it represents the return type of a function that always throws an error.

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
- The declared variable is available from the block is enclosed in.

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
- To define an object type, we list its properties and their types.
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
interface Cat{
    name: string;
    breed: string;
}

function makeCat(name: string, breed: string): Readonly<Cat> {
    return { name, breed };
}

const mia = makeCat("Mia", "Calico");
// mia.breed = "Tabby"; // error

// OR add `readonly` in front of the name to make it read only
// interface Cat{
//     readonly name: string;
//     breed: string;
// }
```

- readonly tuple:= `readonly [number, number, number]`

- readonly array:= `const constArr = [1, 2] as const;

### 4.10 `null` and `undefined`

- These primitive values are used to signal absent or uninitialized value.

```typescript
let u: undefined = undefined;
let n: null = null;
```

### 4.11 Tuples

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

```typescript
type ThreeDCoordinate = [ x: number, y: number, z: number ];

function add3DCoordinate(c1: ThreeDCoordinate, c2: ThreeDCoordinate): ThreeDCoordinate {
    return [
        c1[0] + c2[0],
        c1[1] + c2[1],
        c1[2] + c2[2],
    ]
}

console.log(add3DCoordinate([0, 10, 0], [10, 20, 30])); // [ 10, 30, 30 ]
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

- Key distinction is that a `type` cannot be reopened to add new properties, whereas an `interface` is always extendable.
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

- A type alias is literally that - a name for any type.

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

#### 6.2.2 Numeric literal type

```typescript
function rollDice(times: 1 | 2): void {
    for (let i=0;i<times;i++) {
        let dice: number = Math.floor((Math.random() * 5) + 1);
        console.log(dice);
    }
}
rollDice(2);
```

#### 6.2.3 Type casting

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

- Refining types to more specific types than declared is called narrowing.

```typescript
function padLeft(padding: number | string, input: string) {
  if (typeof padding === "number") {
    return " ".repeat(padding) + input; // padding:= number
  }
  return padding + input; // padding:= string
}
```

## 10. Type predicate

- To define a user-defined type guard, we simply need to define a function of which return type is a type predicate:

```typescript
let pet = getSmallPet();

if (isFish(pet)) {
  pet.swim();
} else {
  pet.fly();
}
```

## 11. Parameters

### 11.1 Rest parameters

- It allows you to represent an indefinite number (zero or more) of arguments as an array.

```typescript
function <function_name>(...<parameter_name>: <parameter_type>[]) { }
```

- Rules:
  - A function has only one rest parameter.
  - The rest parameter appears last in the parameter list.
  - The type of the rest parameter is _array_.

### 11.2 Default parameters

- The default initialised value for the _omitted_ parameters.
- Default parameters don't need to appear after the required parameters. When a default parameter appears before a required parameter, you need to explicitly pass `undefined` to get the default initialised value.

```typescript
function <function_name>(<parameter_name>: <parameter_type>=<default_value>,...): <return_type_if_any>{ }
```

### 11.3 Optional parameters

- Optional parameters must come after the required parameters.
- Using `?` after the parameter name makes a function parameter optional.

```typescript
function <function_name>(<parameter_name>?: <parameter_type>=<default_value>,...): <return_type_if_any>{ }
```

## 12. Class

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

### 12.1 Getters and setters

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

### 12.2 Member visibility

- `private`, `protected` and `public`.

### 12.3 Abstract class

- It defines common behaviours for derived classes to extend.
- Unlike a regular class, it cannot be instantiated directly.
- To use it, you must inherit and implement its abstract methods.
- It often contains one or more abstract methods.

```typescript
abstract class PokemonCharacter {
    constructor() {}

    walk() {}
    attack() {
        console.log(`${this.name} attack with ${this.getSpecialAttack()}`);
    }

    abstract getSpecialAttack(): string;
    abstract get name(): string;
}

class Pikachu extends PokemonCharacter {
    get name(): string {
        return "Pikachu";
    }
    getSpecialAttack(): string {
        return "Thunder Shock";
    }
}

const pikachu = new Pikachu();
pikachu.attack();
```

## 13. Static methods and properties

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

## 14. Operators

### 14.1 Non-null assertion operator `!`

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

### 14.2 Nullish coalescing operator `??`

- `??` returns the first argument if not `null`/`undefined`. Otherwise, it returns the second one.

```typescript
a ?? b // equals to
( a!== null && a!== undefined ) ? a : b
```

### 14.3 `in`

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

### 14.4 `instanceof`

- It has an operator for checking whether or not a value is an “instance” of another value.

## 15. Callback functions

- A `callback` is used to pass a function to another function. So that within the called function, it can _call back_ the function you passed to it.

```typescript
interface Greeter {
  (message: string): void;
}

function sayHi(callback: Greeter) {
  callback('Hi!');
}

const myGreeter: Greeter = (message: string) => {
  console.log(`Greeting: ${message}`);
};

sayHi(myGreeter); // "Greeting: Hi!"
```

## 16. Optionals

```typescript
function printIngredient(quantity: string, ingredient: string, extra?: string) {
    console.log(`${quantity} ${ingredient} ${extra ? ` ${extra}` : ""}`);
}

printIngredient("1C", "Flour");
printIngredient("1C", "Sugar", "Something more")

interface User {
    id: string;
    info?: {
        email?: string;
    }
}

function getEmailEasy(user: User): string {
    return user?.info?.email ?? "";
}

function addWithCallback(x: number, y: number, callback?: () => void) {
    console.log([x,y]);
    callback?.();
}
```

## 17. Types

### 17.1 Generics

- Generics can create a component that can work over a variety of types rather than a single one.

```typescript
function identity<Type>(arg: Type): Type {
  return arg;
}

function identityArr<Type>(arg: Type[]): Type[] {
  console.log(arg.length);
  return arg;
}
```

```typescript
function simpleState<T>(initial: T): [() => T, (v: T) => void] {
    let val: T = initial;
    return [
        () => val,
        (v: T) => {
            val = v;
        },
    ];
}

const [str1getter, str1setter] = simpleState("hello");
console.log(str1getter()); // hello
str1setter("bye");
console.log(str1getter()); // bye

const [int1getter, int1setter] = simpleState(1);
console.log(int1getter()); // 1
int1setter(2);
console.log(int1getter()); // 2
```

### 17.2 `keyof` Type Operator

- The `keyof` operator takes an object type and produces a string or numeric literal union of its keys.

```typescript
function extract<DataType, KeyType extends keyof DataType>(
    items: DataType[],
    key: KeyType
): DataType[KeyType][] {
    return items.map((item) => item[key]);
}

const people = [
    { name: 'Bob', age: 20},
    { name: 'Alice', age: 30}
]

console.log(extract(people, "age"));
console.log(extract(people, "name"));
```

### 17.3 `typeof` Type Operator

- `typeof` shows the type of values we have at runtime.

```typescript
function f() {
  return { x: 10, y: 3 };
}
type P = ReturnType<typeof f>; // type P = { x: number; y: number; }
```

### 17.4 Indexed Access Types

- An indexed access type can look up a specific property on another type.

```typescript
type Person = { age: number; name: string; alive: boolean };
type Age = Person["age"]; // type Age = number
```

### 17.5 Conditional Types

- They help describe the relation between the types of inputs and outputs.

```typescript
// SomeType extends OtherType ? TrueType : FalseType;
```

### 17.6 Mapped Types

- As a generic type, it uses a union of `PropertyKey`s (frequently created via a keyof) to iterate through keys to create a type:

```typescript
// definition
type OptionsFlags<Type> = {
  [Property in keyof Type]: boolean;
};

type Features = {
  darkMode: () => void;
  newUserProfile: () => void;
};
 
type FeatureOptions = OptionsFlags<Features> // type FeatureOptions = { darkMode: boolean; newUserProfile: boolean; }
```

- Key remapping via `as`:

```typescript
// definition
type MappedTypeWithNewProperties<Type> = {
    [Properties in keyof Type as NewKeyType]: Type[Properties]
}

//

type Getters<Type> = {
    [Property in keyof Type as `get${Capitalize<string & Property>}`]: () => Type[Property]
};
 
interface Person {
    name: string;
    age: number;
    location: string;
}
 
type LazyPerson = Getters<Person>; // type LazyPerson = { getName: () => string; getAge: () => number; getLocation: () => string; }
```

### 17.7 Template Literal Types

- They are build on string literal types and can expand into many strings via unions.

```typescript
type Size = 'small' | 'medium';
type Colour = 'red' | 'blue';
type Style = `${Size}-${Colour}`;

function applyStyle(style: Style) {
}

applyStyle('small-primary');
```

## 18. Utility Types

- They facilitate common type transformations.

### 18.1 `Awaited<Type>`

- It extracts the type that is being returned by a promise. It helps us to avoid using `.then()` and `await` the same promise repeatedly.

```typescript
async function getCat(): Promise<{ 
    name: string; 
    age: number 
}> {
    return { name: "Simba", age: 1 };
}
  
type CatType = Awaited<ReturnType<typeof getCat>>; // [ name: string, age: number ]
```

### 18.2 `Capitalize<StringType>`

- It converts the first character into the string to an uppercase equivalent.

```typescript
type LowercaseGreeting = "hello, world";
type Greeting = Capitalize<LowercaseGreeting>; // "Hello, world"
```

### 18.3 `ConstructParameters<Type>`

- It constructs a tuple or an array type from the types of a constructor function type.

```typescript
class MyClass {
  constructor(x: number, str: string) {}
}

type T0 = ConstructorParameters<typeof MyClass>; // [ x: number, str: string ]
```

### 18.4 `Exclude<UnionType, ExcludedMembers`

- It constructs a type by excluding all union members that are assignable to `ExcludedMembers`.

```typescript
type ExcludedType = Exclude<"a" | "str", "str">; // "a"
```

### 18.5 `Extract<Type, Union>`

- It constructs a new type by exracting all union members that are assignable to `Union`. It is the opposite of `Exclude`.

```typescript
type ExtractedType = Extract<"a" | "str", "str">; // "str"
```

### 18.6 `InstanceType<Type>`

- It constructs a type consisting of the instance type of a constructor function in Type. It is similar to `ReturnType`, but it acts on a class constructor.

```typescript
class Cat {
  name: string;
  age: number;

  constructor(cat: { name: string; age: number }) {
    this.name = cat.name;
    this.age = cat.age;
  }
}

type CatType = InstanceType<typeof Cat>; // [ name: string; age: number ]
```

### 18.7 `Lowercase<StringType>`

- It converts each character into the string to the lowercase equivalent.

```typescript
type Greeting = "Hello, world";
type QuietGreeting = Lowercase<Greeting>; // "hello, world"
```

### 18.8 `NonNullable<Type>`

- It constructs a new type by excluding `null` and `undefined`.

```typescript
type Type = string | number | null | undefined;

type NonNullableType = NonNullable<Type>; // "string" | "number"
```

### 18.9 `Omit<Type, Keys>`

- It constructs a type by picking all properties from Type, then removing Keys. It is the opposite of `Pick`.

```typescript
type Type = { a: number, str: string };

type OmitType = Omit<Type, "a">; // { str: string }
```

### 18.10 `Parameters<Type>`

- It constucts a tuple types from the types used in the parameters of a function type `Type`.

```typescript
const sayHi = (str: string) => {
  console.log("Hi");
};

type FunctionParameters = Parameters<typeof sayHi>; // [str: string]
```

### 18.11 `Partial<Type>`

- It constructs a type with all properties of Type set to optional.

```typescript
type Type = { a: number, str: string };

type PartialType = Partial<Type>; // { a?: number; str?: string }
```

### 18.12 `Pick<Type, Keys>`

- It constructs a type by picking the set of properties Keys from Type.

```typescript
type Type = { a: number, str: string };

type PickType = Pick<Type, "a">; // { a: number }
```

### 18.13 `Readonly<Type>`

- It creates a new type with all properties of Type set to `readonly`.

```typescript
type Type = { a: number, str: string };

type ReadonlyType = Readonly<Type>; // { readonly a: number; readonly str: string }
```

### 18.14 `Record<Keys, Type>`

- It constructs an object type of which property keys are Keys and of which property values are Type.

```typescript
interface CatInfo {
  age: number;
  breed: string;
}

type CatName = "puffy" | "mia";

const cats: Record<CatName, CatInfo> = {
  puffy: { age: 1, breed: "Persian" },
  mia: { age: 2, breed: "Stray" }
};

console.log(cats.puffy); // { "age": 1, "breed": "Persian" }
```

### 18.15 `Required<Type>`

- It constructs a type consisting of all properties of Type set to required. It is the opposite of `Partial`.

```typescript
type Type = { a?: number, str?: string };

type RequiredType = Required<Type>; // { a: number; str: string }
```

### 18.16 `ReturnType<Type>`

- It constructs a type of the return type of the function. (Use in `useState` hook in React)

```typescript
const getCat = () => ({
  name: "Simba",
  age: 1
});

type FunctionReturnType = ReturnType<typeof getCat>; // { name: string; age: number; }
```

### 18.17 `Uncapitalize<StringType>`

- It converts the first character into the string to a lowercase equivalent.

```typescript
type UppercaseGreeting = "HELLO WORLD";

type UncomfortableGreeting = Uncapitalize<UppercaseGreeting>; // "hELLO WORLD"
```

### 18.18 `Uppercase<StringType>`

- It converts each character into the string to the uppercase version.

```typescript
type Greeting = "Hello, world";

type ShoutyGreeting = Uppercase<Greeting>; // "HELLO, WORLD"
```

## 19. Design patterns

### 19.1 Singleton

```typescript
class Flower {
    constructor(public readonly name: string, public readonly numberOfPetals: number) {
    }
}

class FlowerList {
    private flowers: Flower[] = [];

    static instance: FlowerList = new FlowerList();

    private constructor() {}

    static addFlower(flower: Flower) {
        FlowerList.instance.flowers.push(flower);
    }

    getFlowers() {
        return this.flowers;
    }
}

FlowerList.addFlower(new Flower("Rose", 20));
console.log(FlowerList.instance.getFlowers());
```
