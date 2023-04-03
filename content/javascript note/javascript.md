---
title: JavaScript for beginners
description: JavaScript for beginners
summary: "Updated by Fatma, Mar 28, 2023."
date: 28-03-2023
categories:
  - "Coding"
tags:
  - "javascript"
  - "coding"
  - "algorithms"
  - "data structures"
---

![header](/img/javascript_header.png)

- A dynamic language with types and operators, standard built-in objects, and methods.
- It supports object-oriented programming with object prototypes, instead of classes.
- It supports functional programming - because they are objects, functions may be stored in variables and passed around like any other object.

## Types

- **Number:** double-precision 64-bit format IEEE 754 values
- String
- Boolean
- Object
  - Function
  - Array
  - Date
  - RegExp
- Symbol
- undefined
- null
- Error

- There is no such thing as an integer except `BigInt`.

## Numbers

- `Math.sin(3.5);`
- `Math.PI;`
- You can convert a string to an integer. You should always provide as below:
  - `parseInt('123', 10);` # 10 is the base.
- Unlike parseInt(), parseFloat() always uses base 10.
- isNaN(NaN); # to test whether it is numeric.
- Infinity and -Infinity exist. You can test:
  - isFinite(1/0);

## Strings

- `'hello'.length;`
- `'hello'.charAt(0);`
- `'hello, world'.replace('world', 'mars');`
- `'hello'.toUpperCase();`

## Check null objects

```javascript
// It means whether they will execute their second operand is dependent on the first.
var name = o && o.getName();
var name = cachedName || (cachedName = getName());
```

## Comparison

```javascript
123 == '123'; // true
1 == true; // true

123 === '123' // false
1 === true; // false
```

## Conditional

```javascript
var allowed = (age > 18) ? 'yes' : 'no';
```

## do while

```javascript
var input;
do {
  input = get_input();
} while (inputIsNotValid(input));
```

## for

```javascript
for (let myLetVariable = 0; myLetVariable < 5; myLetVariable++) {}

for (var myLetVariable = 0; myLetVariable < 5; myLetVariable++) {}

for (let value of array) {}

for (let property in object) {}

for (var i = 0; i < a.length; i++) {}
```

## for each

```javascript
['dog', 'cat', 'hen'].forEach(function(currentValue, index, array)) {});
```

## if

```javascript
var name = 'kittens';
if (name == 'puppies') {
  name += ' woof';
} else if (name == 'kittens') {
  name += ' meow';
} else {
  name += '!';
}
name == 'kittens meow';
```

## makePerson

```javascript
function personFullName() {
  return this.first + " " + this.last;
}

function personFullNameReversed() {
  return this.last + " " + this.first;
}

function Person(first, last) {
  this.first = first;
  this.last = last;
  this.fullName  = personFullName;
  this.fullNameReversed = personFullNameReversed;
}

var s = new Person('Simon', 'Willison');
```

## Object

```javascript
var obj = new Object;
// or
var obj = {};

// the core of JSON format
var obj = {
  name: 'Carrot',
  _for: 'Max', // since for is a reserved word, _for is used instead.
  details: {
    color: 'orange',
    size: 12
  }
};

// Attribute access
obj.details.color; // orange
obj['details']['size']; // 12

obj.name = 'Simon';
var name = obj['name'];

var user = prompt('what is your key?')
obj[user] = prompt('what is its value?')

////

var person = Object.create(Object.prototype);
person.firstName = "Paul";
person.lastName  = "Irish";
```

## Object prototype

```javascript
function Person(name, age) {
  this.name = name;
  this.age = age;
}

// Define an object
var you = new Person('You', 24);
```

## Function

- Along with the objects, functions are the core components.

```javascript
// If no return statement is used, it returns undefined.
function add(x, y) {
  var total = x + y;
  return total;
}

// You can also pass in more arguments than the function is expecting.
add(2, 3, 4); // 5

// You can't perform addition on undefined.
add(); // NaN

////

// function avg(...numbers)

// function avg() { arguments[i]... }

function avg(arr) {
  var sum = 0;
  for (var i = 0, j = arr.length; i < j; i++) {
    sum += arr[i];
  }
  return sum / arr.length;
}

avg([2, 3, 4, 5]); // 3.5

// if you want to call a function with an arbitrary array of arguments
avg.apply(null, [2, 3, 4, 5]);

// anonymous function the same as avg function above
var avg = function() {
  var sum = 0;
  for (var i = 0, j = arguments.length; i < j; i++) {
    sum += arguments[i];
  }
  return sum / arguments.length;
};
```

## Other Types

- null := non-value
- undefined := uninitialized value
- false:= "", 0, NaN, null, undefined, false
- true:= all the remainings.

## Variables

### let

- It allows you to declare block-level variables.
- The declared variable is available from the block it is enclosed in.
- `let a;`
- `let name = 'Simon';`

### const

- `const` variables are never intended to change.
- `const Pi = 3.14;`

### var

- `var a;`
- `var name = 'Simon';`

## Operators

- +, -, *, /, %
- +=, -=
- !=, !=== # The second one is for strict comparisons.

## Objects

- A simple collection of name-value pairs. It is similar to dictionaries in python.

## Array

- A special type of objects
- It is resizable and can contain a mix of different data types.
- Its elements must be accessed by a nonnegative integer as an index.
- Array-copy operations create shallow copies.

```javascript
var a = ['dog', 'cat', 'hen']; // OR

var a = new Array();
a[0] = 'dog';
a[1] = 'cat';
a[2] = 'hen';

a.length; // 3
a.push(item1, item2);
a.toString();
a.join(sep);
a.pop();
a.slice(start[, end]);
a.reverse();
```

### Custom Objects

- JS contains no class statement.
- JS uses functions as classes.

## Class

- Class is a template for creating objects.
- Classes are built on prototypes.
- Classes are special functions.

### Class declaration

- It is a way to define a class.

### Class expression

- It is another way to define a class.
- Class expressions can be named or unnamed.

## Core primitive

```javascript
function hello(thing) {
  console.log(this + " says hello " + thing);
}

// The first parameter is thisValue := Bob (here)
hello.call("Bob", "world") //=> Bob says hello world

// We invoked the hello method with this set to "Bob" and a single argument "world".
// This is the core primitive of JavaScript function invocation.
```

## Arrow function

- It is a compact alternative to a traditional function expression, but it is not unlimited to use in all situations.
- Differences and Limitations:
  - It doesn't have its bindings to `this` or `super`, and shouldn't be used as a method.
  - It does not have arguments or `new.target` keywords.
  - It isn't suitable for `call`, `apply`, and `bind` methods, which generally rely on establishing a scope.
  - It cannot be used as a constructor.
  - It cannot use `yield`, within its body.

```javascript
const materials = [' Hydrogen', 'Helium'];

console.log(materials.map(material => material.length)); // [8, 6]

function (a) {
  return a + 100;
}

(a) {
  return a + 100;
}

(a) => a + 100;

a => a + 100;

function (a, b) {
  return a + b + 100;
}

(a, b) => a + b + 100;

let a = 4;
let b = 2;

function () {
  return a + b + 100;
}

let a = 4;
let b = 2;

() => a + b + 100;

function (a, b){
  let chuck = 42;
  return a + b + chuck;
}

(a, b) => {
  let chuck = 42;
  return a + b + chuck;
}

function bob (a){
  return a + 100;
}

let bob = a => a + 100;

(param1, paramN) => {
   let a = 1;
   return a + param1 + paramN;
}

(a=400, b=20, c) => expression
```

## Document Object Model (DOM)

- When a web page is loaded, the browser creates a Document Object Model of the page.

- With the object model:
  - It can change all the HTML elements on the page.
  - It can change all the HTML attributes on the page.
  - It can change all the CSS styles on the page.
  - It can remove existing HTML elements and attributes.
  - It can add new HTML elements and attributes.
  - It can react to all existing HTML events on the page.
  - It can create new HTML events on the page.

  - DOM defines a standard for accessing documents.

  - The parts of DOM:
    - Core DOM - standard model for all document types
    - XML DOM - standard model for XML documents
    - HTML DOM - standard model for HTML documents

- DOM defines
  - HTML elements as objects
  - Properties of all HTML elements
  - Methods to access all HTML elements
  - Events for all HTML elements

## Property

- A property has a name and value.
- It can be:
  - **enumerable:** for(prop in obj)
  - **writable:** You can replace it.
  - **configurable:** You can delete it or change its other attributes.
- We can add a property to an object using `Object.defineProperty`.

```javascript
// Create the simplest object
var person = Object.create(null);

person['name'] // undefined

person.name // undefined

////

var Person = Object.create(null);

Object.defineProperty(person, 'firstName', {
  value: "Bob",
  writable: true,
  enumerable: true,
  configurable: true
});

Object.defineProperty(person, lastName, {
  value: "Alice",
  writable: true,
  enumerable: true,
  configurable: true
});

////

// OR

////

// Eliminate the common defaults
var config = {
  writable: true,
  enumerable: true,
  configurable: true
};

var defineProperty = function(obj, name, value) {
  config.value = value;
  Object.defineProperty(obj, name, config);
};

var person = Object.create(null);
defineProperty(person, 'firstName', "Bob");
defineProperty(person, 'lastName', "Alice");
```

---

## Prototype

- Objects are pairs of keys and values, like `python`'s dictionary.
- The prototype of an object is a pointer to another object.
- If you try to look up a key on an object and it is not found, it will look for it in the prototype. It will follow the "prototype chain" until it sees a null value. In that case, it returns undefined.
- You can look up an object's prototype by using `Object.getPrototypeOf(<object_name>);`

```javascript
var person = Object.create(null);
defineProperty(person, 'fullName', function() {
  return this.firstName + ' ' + this.lastName;
});

var man = Object.create(man);
defineProperty(man, 'sex', 'male');

var bob = Object.create(man);
defineProperty(bob, 'firstName', 'Bob');
defineProperty(bob, 'lastName', 'Alice');

bob.sex // male
bob.fullName() // Bob Alice

// OR //

var person = Object.create(null);

person['fullName'] = function() {
  return this.firstName + ' ' + this.lastName;
};

var man = Object.create(man);
bob['firstName'] = "Bob";
bob['lastName'] = "Alice";

bob.sex // male
bob.fullName() // Bob Alice
```

### `Array.prototype.map()`

- It is an iterative method that calls a provided `callbackFn` function once for each element in an array and constructs a new array from the results.

```javascript
const numbers = [1, 4, 9];
const roots = numbers.map((num) => Math.sqrt(num)); // roots := [1, 2, 3]

const arr = [ {key: 1, value: 10} ]; // [{key: 1, value: 10}]
const newArr = arr.map(({key, value}) -> ({ [key]: value })); // [{1: 10}]
```

---

## while

```javascript
while (true) {}
```

---

## switch

```javascript
switch (action) {
  case 'draw':
    drawIt();
    break;
  case 'eat':
    eatIt();
    break;
  default:
    doNothing();
}
```

---

## typeof

```javascript
// If you try to access a non-existent array index.
typeof a[90]; // undefined
```
