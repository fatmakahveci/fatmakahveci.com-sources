---
title: Go for beginners
description: Go for beginners
summary: "Go for beginners"
date: 02-03-2023
categories:
  - "Coding"
tags:
  - "go"
  - "coding"
  - "algorithms"
  - "data structures"
---

![go](/img/go.png)

- Go (Golang) is a feature-rich, compiled, strongly-typed and garbage-collected programming language born from Google.
- Go is popularly used in network, system tools, database development, and block chain.
- The main selling points of Go are being flexible as many dynamic script languages, memory saving, fast program warming-up, code execution speed, concurrent programming, cross-platform support, stable core design, stack management, active community, code readability, and fast compilation.
- It has explicit support for concurrent programming that gets the most out of multicore and networked machines.
- A Go file consists of the following parts:
  - Package declaration
  - Import packages
  - Functions
  - Statements and expressions

- Advantages of Go executables are
  - small memory footprint,
  - fast code execution, and
  - short warm-up duration.

- [Go's official website](https://go.dev/)
- [Go's official documentation](https://go.dev/doc/)
- [Libraries](https://github.com/avelino/awesome-go)

- **Gophers** means Go programmers.
- **gc** is abbreviation for Go compiler.

---

## 1. Hello world

### 1.1. Download and install Go

- Visit the [Go](https://go.dev/doc/install)'s download page.
- You can test the installation:

```bash
go version
```

- You can use the following IDEs:
  - [JetBrains GoLand](https://www.jetbrains.com/go/download/#section=mac)
  - [Visual Studio Code](https://code.visualstudio.com/Download)
  - [Atom](https://github.blog/2022-06-08-sunsetting-atom/)
  - [Sublime Text](https://www.sublimetext.com/)

#### 1.1.1. Directories

- `$GOPATH` and `$GOROOT` are environment variables that define a certain arrangement and organization for the Go source code.
  - Go code belongs to `$GOPATH` workspace directory comprised of 3 subdirectories:
    - `src` holds the source code.
    - `pkg` holds package objects.
    - `bin` holds compiled commands.
  - `$GOROOT` is for compiler and tools that come from go installation and is used to find the standard libraries.

### 1.2. Create a directory for the project

```bash
mkdir hello_world
cd hello_world
```

Programs start running in `package main`. The main packages are not importable.

```go
// file: main.go
package main

import "fmt"

func main() { // Many `{` can't be put on the next line because a syntax error occurs.
  fmt.Println("Hello World")
}
```

### 1.2.1. Build and run

- `go run` quickly runs a Go program without generating an executable binary. It is just a convenient way to run simple Go programs.

- For large Go projects, use `go build` or `go install` to build then run executable binary files instead.
  - `go build` compiles the packages, along with their dependencies, but it doesn't install the results.
  - `go install` compiles and installs the packages.

### 1.2.2. Other basic commands

- `go fmt` formats source code with a consistent coding style.

- `go vet` examines source code and reports suspicious constructs, such as Printf calls whose arguments do not align with the format string. Vet uses heuristics that do not guarantee all reports are genuine problems, but it can find errors not caught by the compilers.

- `go test` command to run tests and benchmarks.

- `go.mod` manages dependencies without relying on external package managers.
  - `go mod init [<module_path>]` generates a `go.mod` file.
  - `go mod tidy` adds missing module dependencies into and remove unused dependencies from the `go.mod` file.

- `go get` adds, upgrades, downgrades, or removes a single dependency.

- `go help <subcommand>` views the help message for given `<subcommand>`.

---

- `go doc` extracts and generates documentation.
- It runs as a web server and presents the documentation as a web page.

```bash
# Install godoc
go install golang.org/x/tools/cmd/godoc@latest

godoc -http=:6060 &
```

Go to `http://localhost:6060/`

```go
go doc <package_name>
go doc <package_name>.<function_name>
```

---

## 2. Packages

- Packages organizes codes.
- A package must import another package to use the exported code elements.
- In Go, codes should be organized into packages by their functionalities.
- A `package` is a directory containing `.go` file(s).
- You should divide your code into multiple files for readability.

### 2.1. Naming

- Package names should be unique, short (often simple nouns), singular, and lowercase. It provides context for its contents.
- A Go package has both a name and a path. By convention, the last element of the package path is the package name.
- You can abbreviate a package name if it is familiar to the programmer.
- You can locally rename the package names to import multiple packages with the same name.

```go
package <package_name>

import "<package_name>" // importing a single package

// importing multiple packages (option 1)
import "<package_name>"
import "<package_name>"

// importing multiple packages (option 2)
import (
  "<package_name>"
  "<package_name>"
)

// package aliases
import <package_alias> "<package_name>"
<package_alias>.<function_name>() // instead of <package_name>.<function_name>()

// Single-line comment

/* Multi-line
   comment
   (Block comment)
 */
```

### 2.2. Standard packages

- Go comes with a `math`, `net` (networking), `fmt` (formatted IO), etc.

[Ref](https://pkg.go.dev/std)

### 2.3. Managing dependencies

- Dependencies are external packages that your code utilizes. As you continue to work on the code, an upgrade or substitution of these dependencies may be required.
- Go's dependency managers keep your Go applications secure and consistent as you work with the dependencies.
- Go edits [go.mod](https://go.dev/doc/modules/gomod-ref) file to manage dependencies.
- Each formal Go project supporting Go modules needs a `go.mod` file located in the root folder of that project.

---

## 3. Functions and Methods

### 3.1. Functions

- Functions can take zero or more arguments.
- `x int, y int` can be written as `x, y int` if the types are the same.

- The type comes after the variable name. i.e. `func <function_name>(<variable_name> <type>)`

```go
// Declaring a function
func <function_name>(<args>) {
}

// Calling a function
<function_name>(<args>)
```

- A function can return any number of values.
- You can use _blank identifier_ (`_`) to ignore a declared but not used variable.

```go
package main
 
import "fmt"

func main() {
    num, _ := returnTwoNumbers()
    fmt.Println(num)
}
 
func returnTwoNumbers() (int, int) {
    return 1, 2
}
```

- _Naked return_ is a return statement without arguments that returns the named return values. It harms readability in long functions.

```go
package main
 
import "fmt"

func main() {
    num := divide(2)
    fmt.Println(num)
}
 
func divide(sum int) (x int) {
  x = sum / 2
  return // returns x
}
```

#### 3.1.1. Call-by-value and call-by-reference

```go
package main

import "fmt"

// Call-by-value
func increaseByValue(num int) {
  num = num + 1
}

// Call-by-reference
func increaseByReference(num *int) {
  *num = *num + 1
}

func main() {
  var x int = 3
  fmt.Printf("x = %d (before by value)\n", x) // x = 3
  increaseByValue(x)
  fmt.Printf("x = %d (by value)\n", x) // x = 3

  x = 3
  fmt.Printf("x = %d (before by reference)\n", x) // x = 3
  increaseByReference(&x)
  fmt.Printf("x = %d (by reference)\n", x) // x = 4
}
```

#### 3.1.2. Anonymous functions

- You can assign a function to a variable or even invoke it immediately. Below `getSum` is an example.

```go
package main
 
import "fmt"
 
func main() {
  getSum := func(num1, num2 int) (int) {
    return num1 + num2
  }
  fmt.Printf("1 + 2 = %d", getSum(1, 2))
}
```

##### 3.1.2.1. Immediate invocation of a function

```go
func(word string) {
  fmt.Printf("Hello, %s", word)
} ("World") // prints "Hello World"
```

#### 3.1.3. Function closures

- A `first class function` can be assigned to variables, passed as an argument and can be returned from another function.

- A closure is a nested function that helps us access the outer function's variables even after the outer function is closed.

```go
package main

import "fmt"

func adder() func(int) int { // function returning another function
 sum := 0
 return func(x int) int {
  sum += x
  return sum
 }
}

func main() {
 pos, neg := adder(), adder() // Each closure is bound to its own sum variable.
 for i := 1; i < 4; i++ {
  // pos: 1 3 6
  // neg: -2 -6 -12
  fmt.Println(pos(i), neg(-2*i))
 }
}
```

#### 3.1.4. Defer

- `defer` will move the execution of the statement to the very end inside a function.

- Multiple `defer` statements are allowed.
- Deferred function calls are pushed onto a stack so they follow the LIFO order.

```go
defer fmt.Println("Second")
defer fmt.Println("First")
// Output: First Second
```

### 3.2. Methods

- There is no class in Go, but you can define methods on types.
- A method is a function with a special receiver argument.
- A method can return any number of values.

```go
func (<receiver>) <func_name> (<>) {
  // code
}
```

#### 3.2.1. Methods on struct and non-struct types

```go
package main

import (
  "fmt"
  "math"
)

// 1*: Methods on struct
type Vertex struct {
  X, Y float64
}

func (v Vertex) Abs() float64 {
  return math.Sqrt(v.X*v.X + v.Y*v.Y)
}
//

// 2*: Methods on non-struct types
type MyFloat float64

func (f MyFloat) Abs() float64 {
  if f < 0 {
    return float64(-f)
  }
  return float64(f)
}
//

func main() {
  // 1*
  v := Vertex{3, 4}
  fmt.Println(v.Abs())

  // 2*
  f := MyFloat(-math.Sqrt2)
  fmt.Println(f.Abs())
}
```

- A method declaration is restricted to having a receiver whose type is defined within the same package.

#### 3.2.2. Pointer receivers

- You can declare methods with pointer receivers.

```go
func (<*Type>) <func_name> (<>) { // Type cannot itself be a pointer.
  // code
}
```

- Pointer receivers are more common than value receivers since methods often need to modify their receiver.

#### 3.2.3. Methods and pointer indirection

```go
package main

import "fmt"

type Vertex struct {
  X, Y float64
}

func (v *Vertex) Scale(f float64) {
  v.X = v.X * f
  v.Y = v.Y * f
}

func ScaleFunc(v *Vertex, f float64) {
  v.X = v.X * f
  v.Y = v.Y * f
}

func main() {
  v1 := Vertex{3, 4}
  v1.Scale(2)
  ScaleFunc(&v1, 2) // v1 := {12 16}

  v2 := &Vertex{3, 4}
  v2.Scale(2)
  ScaleFunc(v2, 2) // v2 := &{12 16}
}
```

---

## 4. Variables

- Short variable declarations (`:=`) can only be used in functions. Variable declaration and assignment must be in the same line.
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

// zero values := variables declared without an explicit initial value are given their zero value.
// - 0 for numerics
// - false for booleans
// - "" for strings

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
```

### 4.1. Types

- Go doesn't restrict where you define the types, so keep types closer to the location used.
- Keeping the core types grouped at the top is often a good practice.

- Type embedding (TODO)
- Type deduction (TODO)

- The number in the type name represents how many bits a value of that type will occupy in memory at run time.
  - e.g. `uint8` occupies 8 bits in memory.

- Type conversions
  - `<type>(<value>)` converts `<value>` to `<type>`.

```go
var i int = 1
var f float64 = float64(i)`
```

- Type inference

```go
c := 3 + 4i // c := complex128
```

#### 4.1.1. Integer types

- If you don't have a specific purpose, you should use `int` to create an integer value.

- Signed integers: `int`, `int8`, `int16`, `int32` (`rune`), `int64`
- Unsigned integers: `uint`, `unit8` (`byte`), `unit16`, `unit32`, `unit64`, `uintptr`

```go
// Formatting integers
var i int = 1
fmt.Printf("%d\n", 1) // Base 10
```

#### 4.1.2. Floating-point types

- `float32`, `float64`
- In memory, all floating-point numeric values in Go are stored in IEEE-754 format.

```go
// Formatting floating numbers
```

#### 4.1.3. Complex types

- `complex64`, `complex128`

#### 4.1.4. Boolean type

- `bool` can be either `true` or `false`.

#### 4.1.5. String type

- `string`

#### 4.1.6. Error type

- `error`

#### 4.1.7. Pointer types

- A pointer can point to a variable of any type including a pointer.

##### 4.1.7.1. Declaring a pointer of type `T`

```go
var <pointer_name> *T
```

- i.e. a pointer of type `int` can be declared as `var p *int`

- Struct fields can be accessed through a struct pointer.

```go
v := Vertex{1, 2}
p := &v
p.X = 3
// v := {1 3}
```

##### 4.1.7.2. Initialization of a pointer

```go
var <pointer_name> *<data_type> = &<address_value>
```

- If you take a pointer of type `T`, the address of the variable that you will give to a pointer will be only of type `T`, not any other type.
- If you use `var`, there is no need to specify the type during the declaration. The type of a pointer variable is inferred by the compiler.
  - `var ptr = &x`
- You can use `:=` to declare and initialize the pointers.
  - `ptr := &x`
- The default value of a pointer is always `nil`.

##### 4.1.7.3. Dereferencing or indirecting operator (*)

- It accesses the value stored in the variable that the pointer points to.

```go
var x = 1
var ptr = &x
// x = 1, &x = 0xAFFFF, ptr = 0xAFFFF, *ptr = 1
*ptr = 2
// x = 2, &x = 0xAFFFF, ptr = 0xAFFFF, *ptr = 2
```

##### 4.1.7.4. Creating a pointer using the built-in new function

- It takes a type as an argument, allocates memory space to accommodate a value of that type, and returns a pointer to it.

```go
ptr := new(int)
*ptr = 1
// ptr = 0xAFFFF, *ptr = 1
```

##### 4.1.7.5. Pointer to pointer

```go
var x = 1 // x = 1, &x = 0xAFFFF
var ptr = &x // ptr = 0xAFFFF, &ptr = 0xAAAAA
var ptr_ptr = &p // ptr_ptr = 0xAAAAA, *ptr_ptr = 0xAFFFF, **ptr_ptr = 1
```

##### 4.1.7.6. No pointer arithmetic in Go

- Go doesn't support arithmetic operations on pointers except comparing two pointers of same type for equality.

```go
var x = 1
var ptr = &x
// var ptr2 = ptr + 1 // compiler error
var ptr2 = &x
if ptr1 == ptr2 {}
```

#### 4.1.8. Array types

- `[n]<type>` := an array of `n` values of type `<type>`
- Arrays are values in Go. An array variable denotes the entire array. It is not a pointer to the first element. Assigning or passing an array value makes a copy of its contents.
- Passing a pointer to the array avoids copying, but it is a pointer to an array, not an array.

```go
// [length] length is defined
// [...] length is inferred
var arr = [2]int{1,2} // var <array_name> = [<array_length>]<data_type>{<values>}
arr := [2]int{1,2} // <array_name> := [<array_length>]<data_type>{<values>} // length is defined
var arr [2]string // var <array_name> [<array_length>]<data_type>
arr[0] = "Go"
```

#### 4.1.9. Slice types

- `[]<type>` := a dynamically-sized flexible sequence of values of specific type `<type>`
- A slice has no specific length, unlike an array.

```go
var sli []int = {1,2} // similar to an array literal but no element count
sli[lo:hi] // It includes the first, but it excludes the last element.
```

- A built-in function `make` can create a slice:
  - `func make([]<type>, <length>, <capacity>) []<type>`

```go
var s []byte
s = make([]byte, 5, 5) // s := []byte{0, 0, 0, 0, 0}
```

#### 4.1.10. Map types

- `map[K][V]` := a collection of key-value pairs with keys of type `K` and values of type `V`

#### 4.1.11. Struct types

- A struct is a composite type that groups together zero or more values of different types into a single object.
- Each field is often composed of a name and a type. It can be accessed as `<struct_name>.<field_name>`.

```go
struct {
  name            string // the same types can be merged. i.e. `name, surname string`
  surname         string
  number_of_items int
}
```

##### 4.1.11.1. Struct tags

- A struct tag is additional meta data information inserted into struct fields.
- Generally, they provide how a field is encoded or decoded from a format.
- They are used in popular packages such as `encoding/json`, etc.

```go
import "encoding/json"

type User struct {
  // When you encode and decode a struct to JSON, keys are given below.
  FirstName string `json:"first_name"` // key := first_name
  Email string // key := Email
}
```

##### 4.1.11.2. Struct literals

```go
type Vertex struct {
  X, Y int
}

var (
  v1 = Vertex{1, 2}  // has type Vertex
  v2 = Vertex{X: 1}  // Y:0 is implicit
  v3 = Vertex{}      // X:0 and Y:0
  p  = &Vertex{1, 2} // has type *Vertex
)
```

#### 4.1.12. Interface types

- `interface{...}` := A set of method signatures, but it is also a type.
- A value of interface type can hold any value that implements those methods.

- Go supports polymorphism, value boxing, and reflection through interfaces.

```go
type Human interface { // Human is a type that has a Think() method.
  Think() string // takes no args, returns a string
}
```

- Go doesn't have `implements` keyword. A type implements an interface by implementing its methods.

```go
package main

import "fmt"

type I interface {
  M()
}

type T struct {
  S string
}

func (t T) M() {
  fmt.Println(t.S)
}

func main() {
  var i I = T{"hello"}
  i.M()
}
```

**1. Explicit interfaces:**

**2. Implicit interfaces:**

**3. Empty interface:**

---

## 5. Keywords

- Keywords are reserved to prevent them from being used as identifiers.
- Go has only 25 keywords:
  1. Declaring code elements: `const`, `func`, `import`, `package`, `type`, `var`
  2. As parts in composite types: `chan`, `interface`, `map`, `struct`
  3. Controling flow of code: `select`, `case`, `else`, `goto`, `switch`, `fallthrough`, `if`, `range`, `continue`, `for`, `return`  `break`, `default`
  4. Modifying function calls: `defer`, `go`

---

## 6. Identifiers

- An identifier is a token which must be composed of
  - Unicode letters,
  - Unicode digits and `_`, and
  - start with either an Unicode letter or `_`.
- `_` := blank identifier

- All names of types, variables, constants, labels, package names and package import names are identifiers.
- Keywords cannot be used as identifiers.

- _Exported identifiers_ start with an upper case letter, similar to `public` in many other languages.
- _Non-exported identifiers_ do not start with an upper case letter, similar to `private` in many other languages.

---

## 7. Flow control statements

### 7.1. Basic control flow

#### 7.1.1. for

```go
// 1 + 2 + 3
sum := 0
for i := 1; i < 3; i++ {
  sum += i
} // sum := 1 + 2 + 3 = 6
```

- `for <init>; <condition>; <post> {}`
  - _init:_ executed before the first iteration. `i := 0`
  - _condition:_ evaluated before every iteration. `i <= 3`
  - _post:_ executed at the end of every iteration. `i++`

- There are no parantheses surrounding the statement.
- `{}` is always required.
- _init_ and _post_ are optional:
  - `for ;<condition>; {}` OR
  - `for <condition> {}`.
- `for {}` is an infinite loop.

#### 7.1.2. if-else

```go
if number < 0 {
  fmt.Println("number is negative")
}
```

```go
if <init>; <condition> {
  // code
} else {
  // code
}
```

- No parantheses surrounding the statement are required.
- `{}` is always required.

- `if` with a `:=` can execute the short statement before the execution.

```go
// threshold variable is in the scope of the `if` statement.
if threshold := 1; x < threshold {
  return x
}
```

#### 7.1.3. switch-case

- Shorter way of `if-else` statements
- It evaluates cases from top to bottom.
- It only runs the first case corresponds to the desired condition, not the followings.
- Cases doesn't need to be constants, and the values doesn't need to be integers.

```go
switch time.Now().Weekday() { // import "time"
  case time.Saturday, time.Sunday: // use `,` for multiple cases
    fmt.Println("It's the weekend")
  default:
    fmt.Println("It's a weekday")
}
```

- `switch {}` is the same as `switch true`.

### 7.2. Control flow for specific types in Go

#### 7.2.1. for-range

For container types

```go
```

#### 7.2.2. type-switch

For interface types

```go
```

#### 7.2.3. select-case

For channel types

```go
```

## 7.3. Jump statements

### 7.3.1. break

```go
```

### 7.3.2. continue

```go
```

### 7.3.3. goto

```go
```

### 7.3.4. fallthrough

```go
```

---

## 8. Memory management

### 8.1. Memory allocation

- Memory allocation and deallocation happens automatically.
- Autonomous implementation of memory usage patterns such as memory pooling, preallocation, etc. avoids making a system call for each memory allocation.
- Whether if an object will be stack or heap allocated is decided by the compiler.

#### 8.1.1. `new()` and `make()`

- Both will allocate and get a memory address.
- `new()` is not initialized. It is so you cannot put any data initially.
- `make()` is more common. It is initialized and non-zeroed storage so you can put data initially.

### 8.2. Garbage collection (GC)

- It happens automatically.
- It allows automatic memory management to make code cleaner and avoid memory leak.
- Out of scope or `nil`

### 8.3. Escape analysis

---

## 9. Concurrency

### 9.1. Goroutine

```go
package main

import (
 "fmt"
 "sync"
 "time"
)

func main() {
 var wg sync.WaitGroup
 wg.Add(1)

 go func() {
  count("sheep")
  wg.Done()
 }()

 wg.Wait()
}

func count(thing string) {
 for i := 1; i <= 5; i++ {
  fmt.Println(i, thing)
  time.Sleep(time.Millisecond * 500)
 }
}
```

### 9.2. Channels and select mechanisms

- to do synchronizations between goroutines.

---

## 10. Iterators

---

## 11. Queues

---

## 12. Sets

---

## 13. Trees

---

## 14. Conditionals

- Syntax      = { Production } .
- Production  = production_name "=" [ Expression ] "." .
- Expression  = Term { "|" Term } .
- Term        = Factor { Factor } .
- Factor      = production_name | token [ "…" token ] | Group | Option | Repetition .
- Group       = "(" Expression ")" .
- Option      = "[" Expression "]" .
- Repetition  = "{" Expression "}" .

---

## 15. Clockwise/Spiral rule

It is a technique to parse any `C` declaration. There are three steps:

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

Updated by _Fatma_ on February 22, 2023.
