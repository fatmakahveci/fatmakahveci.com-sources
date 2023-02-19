---
title: Go for beginners
description: Go for beginners
summary: "Go for beginners"
date: 16-02-2023
categories:
  - "Coding"
tags:
  - "go"
  - "coding"
  - "algorithms"
  - "data structures"
---

- Go (Golang) is a strongly-typed and garbage-collected programming language.
- It has explicit support for concurrent programming that gets the most out of multicore and networked machines.
- A Go file consists of the following parts:
  - Package declaration
  - Import packages
  - Functions
  - Statements and expressions

---

## Packages

- In Go, codes should be organized into packages by their functionalities.
- A `package` is a directory containing `.go` file(s).
- You should divide your code into multiple files for readability.

### Naming

- Package names should be unique, short (often simple nouns), singular, and lowercase. It provides context for its contents.
- A Go package has both a name and a path. By convention, the last element of the package path is the package name.
- You can abbreviate a package name if it is familiar to the programmer.
- You can locally rename the package names to import multiple packages with the same name.

```go
package <package_name>

import "<package_name>"

// Single-line comment

/* Multi-line
   comment
 */
```

### Core packages

- `math`, `net` (networking), `fmt` (formatted IO)

---

## Hello world

Programs start running in `package main`. The main packages are not importable.

```go
// file: main.go
package main

import "fmt"

func main() {
  fmt.Println("Hello World")
}
```

Run `go run main.go`

---

## Functions and Methods

- Functions and methods can return multiple values.

### Functions

```go
func <func_name>(<>) {
  
}
```

### Methods

```go
func (<>) <func_name> (<>) {

}
```

---

## Variables

- **Variable types:**
  - Signed integers: `int`, `int8`, `int16`, `int32`, `int64`
  - Unsigned integers: `uint`, `unit8`, `unit16`, `unit32`, `unit64`
  - Floating numbers: `float32`, `float64`
  - `string`
  - `bool`

- `:=` can only be used in functions. Variable declaration and assignment must be in the same line.
- `var` can be used inside and outside of functions.

```go
// initialized value
var name string = "Bob" // var <variable_name> <type> = <value> // type is given
var name = "Bob" // var <variable_name> = <value> // type is inferred

name := "Bob" // <variable_name> := <value> // type is inferred //

// without initial value
var name string
var number int
var isNumber bool

// assign after the initialization
var name string
name = "Bob"
var isNumber bool
isNumber = true

// multiple variables
var name, surname string = "Bob", "Alice"
name, age := "Bob", 20
var (
    name string
    age int = 1
)

// constants
const PIVALUE = 3.14

// Formatting prints
var num = 1.2
var text = "Hello, world!"
fmt.Printf("%v\n", text) // Hello, world!
fmt.Printf("%#v\n", text) // "Hello, world!" // Go-syntax
fmt.Printf("%v%%\n", num) // 1.2%
fmt.Printf("%T\n", i) // float64

// Formatting integers
var i int = 1
fmt.Printf("%d\n", 1) // Base 10
// @TODO

// Formatting floating numbers
// @TODO
```

---

## Types

- Go doesn't restrict where you define the types, so keep types closer to the location used.
- Keeping the core types grouped at the top is often a good practice.

---

## Arrays

```go
// [length] length is defined
// [...] length is inferred
var arr = [2]int{1,2} // var array_name = [length]datatype{values}
arr := [2]int{1,2} // array_name := [length]datatype{values} // length is defined
```

---

## Maps

- .

---

## Conditionals

Syntax      = { Production } .
Production  = production_name "=" [ Expression ] "." .
Expression  = Term { "|" Term } .
Term        = Factor { Factor } .
Factor      = production_name | token [ "…" token ] | Group | Option | Repetition .
Group       = "(" Expression ")" .
Option      = "[" Expression "]" .
Repetition  = "{" Expression "}" .

---

## `godoc`

- It extracts and generates documentation.
- It runs as a web server and presents the documentation as a web page.

```bash
# Install godoc
go install golang.org/x/tools/cmd/godoc@latest

godoc -http=:6060 &
```

Go to `http://localhost:6060/`

---

## Clockwise/Spiral rule

It is a technique to parse any C declaration. There are three steps:

1. Starting with the unknown element, move in a spiral/clockwise direction; when encountering the following replace them with the corresponding English statements:

   - `[X]` or `[]` => Array `X` size of ... or Array undefined size of ...
   - `(type1, type2)` => function passing `type1` and `type2` returning ...
   - `*` => pointer(s) to ...

2. Keep doing this in a spiral/clockwise direction until all tokens covered.

3. Always resolve anything in parantheses first!

  e.g. `str` is an array `10` of `pointers` to `char`.

  ```text
         +-------+
         | +-+   |
         | ^ |   |
    char *str[10];
     ^   ^   |   |
     |   +---+   |
     +-----------+
  ```

  e.g. `fp` is a `pointer` to a `function` passing an `int` and a `pointer` to `float` returning a `pointer` to a `char`.

  ```text
         +--------------------+
         | +---+              |
         | |+-+|              |
         | |^ ||              |
    char *(*fp)( int, float *);
     ^   ^ ^  ||              |
     |   | +--+|              |
     |   +-----+              |
     +------------------------+
  ```

  e.g. `signal` is a `function` passing an `int` and a `pointer` to a `function` passing an `int` returning `nothing` returning a `pointer` to a `function` passing an `int` and returning `nothing`.

  ```text
          +-----------------------------+
          |                  +---+      |
          |  +---+           |+-+|      |
          |  ^   |           |^ ||      |
    void (*signal(int, void (*fp)(int)))(int);
     ^    ^      |      ^    ^  ||      |
     |    +------+      |    +--+|      |
     |                  +--------+      |
     +----------------------------------+
  ```

---

Updated by _Fatma_ on February 16, 2023.
