---
title: Go for beginners
description: Go for beginners
summary: "Updated by Fatma, Mar 28, 2023."
date: 28-03-2023
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
- Go is the contemporary programming language of cloud computing. It is also popularly used in a network, system tools, database development, and blockchain
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
- **gc** is an abbreviation for Go compiler.

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

import (
  "fmt"
)

func main() { // Many `{` can't be put on the next line because a syntax error occurs.
  fmt.Println("Hello World")
}
```

### 1.2.1. Build and run

- `go run` quickly runs a Go program without generating an executable binary. It is just a convenient way to run simple Go programs.

- For large Go projects, use `go build` or `go install` to build and then run executable binary files instead.
  - `go build` compiles the packages, along with their dependencies, but it doesn't install the results.
  - `go install` compiles and installs the packages.

### 1.2.2. Other basic commands

- `go fmt` formats source code with a consistent coding style.

- `go vet` examines source code and reports suspicious constructs, such as Printf calls whose arguments do not align with the format string. The vet uses heuristics that do not guarantee all reports are genuine problems, but it can find errors not caught by the compilers.

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

- Packages organize codes.
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

#### 2.2.1. The `fmt` package

##### 2.2.1.1. Printing: `Print` and `Println`

```go
package main

import (
  "fmt"
)

func main() {
  fmt.Print("Hello", "world") // Helloworld
  fmt.Print("Hello", "world\n") // Hello world\n

  fmt.Println("Hello", "world") // Hello world\n
  fmt.Println("Hello world") // Hello world\n
}
```

- For the details read the documentation: [printing](https://pkg.go.dev/fmt#hdr-Printing)

##### 2.2.1.2. Formatting: `fmt.Sprint()` and `fmt.Sprintln()`

- These format strings without printing.

```go
package main

import (
  "fmt"
)

func main() {
  firstName := "Bob"
  secondName := "Alice"

  name := fmt.Sprintln(firstName, secondName) // name declared but not used
}
```

##### 2.2.1.3. Getting user input `fmt.Scan()`

```go
package main

import (
  "fmt"
)

func main() {
  fmt.Println("What is your name?")

  var name string
  
  fmt.Scan(&name) // &
  fmt.Printf("Nice to meet you %v.\n", name)
}
```

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
 
import (
  "fmt"
)

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
 
import (
  "fmt"
)

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

import (
  "fmt"
)

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
 
import (
  "fmt"
)

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

import (
  "fmt"
)

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

import (
  "fmt"
)

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

#### 3.2.4. Readers

- The `io.Reader` interface represents the read end of a stream of data.
- Some implementations include:
  - files,
  - network connections,
  - compressors,
  - ciphers, etc.
- It has `Read` method, `func (T) Read(b []byte) (n int, err error)`.
  - It populates the given byte slice with data and returns the number of bytes populated and an error value.
  - It returns an `io.EOF` error when the stream ends.

```go
package main

import (
  "fmt"
  "io"
  "strings"
)

func main() {
  r := strings.NewReader("Hello world")

  b := make([]byte, 8)
  for { // while true
    n, err := r.Read(b)
    fmt.Printf("b[:n] = %q\n", b[:n])
    if err == io.EOF {
      break
    }
  }
  // Output =>
  // b[:n] = "Hello wo"
  // b[:n] = "rld"
  // b[:n] = ""
}
```

#### 3.2.5. Images

- It defines the `Image` interface.

```go
package image

type Image interface {
    ColorModel() color.Model
    Bounds() Rectangle
    At(x, y int) color.Color
}
```

- For more details on [Golang Image Processing:](https://golangdocs.com/golang-image-processing)

---

## 4. Variables

- Short variable declarations (`:=`) can only be used in functions. Variable declaration and assignment must be in the same line.
- `var` can be used inside and outside of functions.

- Variables declared without an explicit initial value are given their `zero value`.
  - `0` for numerics
  - `false` for booleans
  - `""` for strings
  - `nil` for maps and channels

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
```

### 4.1. Types

- Go doesn't restrict where you define the types, so keep types closer to the location used.
- Keeping the core types grouped at the top is often a good practice.

- The number in the type name represents how many bits a value of that type will occupy in memory at run time.
  - e.g. `uint8` occupies 8 bits in memory.

- _Type conversion_
  - `<type>(<value>)` converts `<value>` to `<type>`.

```go
var i int = 1
var f float64 = float64(i)`
```

- _Type inference_

```go
c := 3 + 4i // c := complex128
```

- A _type assertion_ provides access to an interface value's underlying concrete value.

```go
package main

import (
  "fmt"
)

func main() {
 var i interface{} = 1

 tr := i.(int)
 fmt.Println(tr) // 1
 
 tr, ok := i.(int) // <value>, <isAssertionSucceed>
 fmt.Println(tr, ok) // 1 true
 
 fa, ok := i.(float32)
 fmt.Println(fa, ok) // 0 false

 fa = i.(float32) // panic will be triggered because i doesn't hold a float32
 fmt.Println(fa)
}
```

- A _type switch_ permits several type assertions in series.

```go
switch v := i.(type) {
  case T:
    // here v has type T
  case S:
    // here v has type S
  default:
    // no match; here v has the same type as i
}
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

- In memory, all floating-point numeric values in Go are stored in IEEE-754 format implemented by all modern CPUs.

- **default:** `float64` occupies 64 bits in memory and provides about 15 digits of precision.
- `float32` occupies 32 bits in memory and provides about 6 digits of precision.

```go
package main

import (
  "fmt"
  "math"
)
func main() {
  fmt.Println(math.MaxFloat32) // the limit for float32 // 3.4028234663852886e+38
  fmt.Println(math.MaxFloat64) // the limit for float64 // 1.7976931348623157e+308
}
```

#### 4.1.3. Complex types

- `complex64`: Components are `float32`.
- `complex128`: Components are `float64`.

- Their equality can be checked by `==` and `!=`.
- `math/cmplx` package is available to work with complex numbers.

```go
package main

import (
  "fmt"
)

func main() {
  var c complex128 = complex(3, 4) // (3+4i)
  fmt.Println(c)
  re := real(c) // real part
  im := imag(c) // imaginary part
  fmt.Println(re, im) // 3 4
}
```

#### 4.1.4. Boolean type

- A `bool` requires 1 byte (8 bits) of memory and represents a Boolean value of `true` or `false`.
- Its zero value is `false`.

```go
package main

import (
 "fmt"
 "strconv"
)

func main() {
 // Boolean operators
 a := 1
 b := 2
 fmt.Println(a == b) // false
 fmt.Println(a != b) // true
 fmt.Println(a < b)  // true
 fmt.Println(a > b)  // false
 fmt.Println(a >= b) // false
 fmt.Println(a <= b) // true

 // Convert string into bool
 var flagBool bool
 flagString := "False"
 flagBool, _ = strconv.ParseBool(flagString)
 fmt.Printf("String: %T, bool: %T\n", flagString, flagBool)

 // Convert bool into string
 var fString string
 fBool := false
 fString = strconv.FormatBool(fBool)
 fmt.Printf("String: %T, bool: %T", fString, fBool)
}
```

#### 4.1.5. String type

- A `string` is an **immutable** sequence of bytes.
- It usually contain human-readable text.
- Text strings are conventionally interpreted as UTF-8-encoded.

```go
package main

import (
 "fmt"
)

func main() {
 s1 := "Hello world"
 fmt.Println(len(s1))      // 11
 fmt.Println(s1[0], s1[3]) // 72 108

 // substrings
 fmt.Println(s1[1:5]) // ello
 fmt.Println(s1[:5])  // Hello
 fmt.Println(s1[7:])  // orld
 fmt.Println(s1[:])   // Hello world

 // s2 holds new string by `+=`
 s2 := "Hello"
 t := s2
 s2 += "world"
 fmt.Println(s2) // Helloworld
 fmt.Println(t)  // Hello

 // Compile error: cannot assign to s2[0] due to in place modification attempt
 s2[0] = 'L'
}
```

#### 4.1.6. Error type

- `error` is a built-in interface type.

```go
// error interface declaration
type error interface {
    Error() string
}
```

- An error is anything that implements the `Error()` method, which returns an error message as a string. `nil` means that no error has occurred.

- In Go built-in errors don't contain stack traces. Also, a conventional try-and-catch block for error handling is not provided in Go. Instead, an error is returned when something unexpected happens.

```go
type DivZero struct{}

func (myerr *DivZero) Error() string{
  return "Cannot divide by 0!"
}
```

- For more details visit "[Effective Error Handling in Golang](https://earthly.dev/blog/golang-errors/)".

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

- Go doesn't support arithmetic operations on pointers except comparing two pointers of the same type for equality.

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

- `[]<type>` is a dynamically-sized flexible sequence of values of specific type `<type>`
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

- Appending to a slice

```go
package main

import "fmt"

func main() {
  var s[]int // []
  s = append(s,1) // [1]
}
```

#### 4.1.10. Map types

- `map[K][V]` is a collection of key-value pairs with distinct keys of type `K` and values of type `V`.
  - The key type `K` must be comparable using `==`.
- A map is a reference to a hash table. It is a dynamic data structure that grows as values are added.

```go
package main

import "fmt"

func main() {
 numberOfCats := make(map[string]int) // creating a map via built-in `make()`
 numberOfCats["Bob"] = 3              // accessing an element
 numberOfCats["Alice"] = 2
 fmt.Println(numberOfCats) // map[Alice:2 Bob:3]
 // equals to
 numberOfCats = map[string]int{ // creating a map via map literals
  "Bob":   3,
  "Alice": 2,
 }
 fmt.Println(numberOfCats) // map[Alice:2 Bob:3]

 // enumerating key/value pairs
 for name, num := range numberOfCats {
  fmt.Printf("%s\t%d\n", name, num)
 } // Bob 3\nAlice 2

 delete(numberOfCats, "Alice") // removes an element
 fmt.Println(numberOfCats)     // map[Bob:3]
}
```

- All of these operations are safe even if the element isn't in the map; a map lookup using a key that isn't present returns the zero value for its type.

- A map element is not a variable and we cannot take its address. One reason that we can't take the address of a map element is that growing a map might cause the rehashing of existing elements into new storage locations, thus potentially invalidating the address.

- We must write a loop to test the equality of two maps.

#### 4.1.11. Struct types

- A struct is a composite type that groups zero or more values of different types into a single object.
- Each field is often composed of a name and a type. It can be accessed as `<struct_name>.<field_name>`.

```go
struct {
  name            string // the same types can be merged. i.e. `name, surname string`
  surname         string
  number_of_items int
}
```

##### 4.1.11.1. Struct tags

- A struct tag is additional metadata information inserted into struct fields.
- Generally, they provide how a field is encoded or decoded from a format.
- They are used in popular packages such as `encoding/json`, etc.

```go
import (
  "encoding/json"
)

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

- `interface{...}` is a set of method signatures, but it is also a type.
- Interfaces are concerned with what a type can do, not the value it holds.
- A value of interface type can hold any value that implements those methods.

- A naming convention for interface types is made with an `-er` suffix: i.e. a talker is anything that talks.

```go
type talker interface {
  talk() string
}
```

- Go supports polymorphism, value boxing, and reflection through interfaces.

- Interfaces are declared with a set of methods that a type must satisfy.

```go
type Human interface { // Human is a type that has a Think() method.
  Talk() string // takes no args, returns a string
}
```

- Go doesn't have `implements` keyword. A type implements an interface by implementing its methods.

```go
package main

import (
  "fmt"
  "math"
)

type shape interface {
  area() float64
}

type square struct {
  length float64
}

type circle struct {
  radius float64
}

func (s square) area() float64 {
  return s.length * s.length
}

func (c circle) area() float64 {
  return math.Pi * c.radius * c.radius
}

func printInfo(s shape) {
  fmt.Printf("Area(%T) = %.1f\n", s, s.area()) // Area(main.square) = 4.0 \n Area(main.circle) = 12.6
}

func main() {
  shapes := []shape{
    square{length: 2.0},
    circle{radius: 2.0},
  }

  for _,s := range shapes { // key, value
    printInfo(s)
  } 
}
```

- _Embedding interface_

```go
type i1 interface {
    m1()
}

type i2 interface {
    m2()
}

type I interface { // embedded interface
    i1
    i2 
}
```

- Go is statically typed thus you cannot have arrays containing values of different types. What it does offer is the empty interface `interface{}` type which allows you to get around some type restrictions that come with a cost.

---

## 5. Operators and punctuations

```text
Precedence        Operator
    5             *  /  %  <<  >>  &  &^
    4             +  -  |  ^
    3             ==  !=  <  <=  >  >=
    2             &&
    1             ||
```

- `+`, `-`, `*` (times, pointer), `/`, `%`
- `&` (address), `|`, `^` (xor), `<<` (left shift), `>>` (right shift), `&^` (and not)
- `+=`, `-=`, `*=`, `/=`, `%=`
- `&=`, `|=`, `^=`, `<<=`, `>>=`, `&^=`
- `&&` (and), `||` (or), `<-` (receive), `++`, `--`
- `==`, `=`, `!` (not), `<`, `>`, `~`
- `!=`, `<=`, `>=`, `...`, `:=`
- `(`, `)`, `[`, `]`, `{`, `}`, `.`, `,`, `:`, `;`

---

## 6. Keywords

- Keywords are reserved to prevent them from being used as identifiers.
- Go has only 25 keywords:
  1. Declaring code elements: `const`, `func`, `import`, `package`, `type`, `var`
  2. As parts in composite types: `chan`, `interface`, `map`, `struct`
  3. Controlling flow of code: `select`, `case`, `else`, `goto`, `switch`, `fallthrough`, `if`, `range`, `continue`, `for`, `return`  `break`, `default`
  4. Modifying function calls: `defer`, `go`

---

## 7. Identifiers

- An identifier is a token which must be composed of
  - Unicode letters,
  - Unicode digits and `_`, and
  - start with either a Unicode letter or `_`.
- `_` := blank identifier

- All names of types, variables, constants, labels, package names and package import names are identifiers.
- Keywords cannot be used as identifiers.

- _Exported identifiers_ start with an upper case letter, similar to `public` in many other languages.
- _Non-exported identifiers_ do not start with an upper case letter, similar to `private` in many other languages.

---

## 8. Flow control statements

### 8.1. for

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

- There are no parentheses surrounding the statement.
- `{}` is always required.
- _init_ and _post_ are optional:
  - `for ;<condition>; {}` OR
  - `for <condition> {}`.
- `for {}` is an infinite loop.

### 8.2. for-range

- It iterates over a slice or map.

```go
package main

import "fmt"

func main() {
  var pow = []int{1, 2, 4}
  for i,num := range pow {
    fmt.Printf("2^%d = %d\n", i, num) // 2^0 = 1\n2^1 = 2\n2^2 = 4
  }
}
```

### 8.3. if-else

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

- No parentheses surrounding the statement are required.
- `{}` is always required.

- `if` with a `:=` can execute the short statement before the execution.

```go
// threshold variable is in the scope of the `if` statement.
if threshold := 1; x < threshold {
  return x
}
```

### 8.4. switch-case

- A shorter way of `if-else` statements
- It evaluates cases from top to bottom.
- It only runs the first case that corresponds to the desired condition, not the following.
- Cases don't need to be constants, and the values don't need to be integers.

```go
switch time.Now().Weekday() { // import "time"
  case time.Saturday, time.Sunday: // use `,` for multiple cases
    fmt.Println("It's the weekend")
  default:
    fmt.Println("It's a weekday")
}
```

- `switch {}` is the same as `switch true`.

- `switch` with a `:=` can execute the short statement before the execution.

```go
// day variable is in the scope of the `switch` statement.
switch day := "Sunday" ; day {
case "Sunday":
  fmt.Println("Enjoy!")
}
```

### 8.5. type-switch

- It is `switch` with types.

```go
package main

import (
  "fmt"
)

func main() {
  var I interface{} = "\"Hello\""
  switch t := I.(type) {
    case int:
      fmt.Printf("%d is an %T.\n", I, t)
    case string:
      fmt.Printf("%s is an %T.\n", I, t)
    default:
      fmt.Println("Unknown")
  }
}
```

### 8.6. break

- `break` terminates the loop when it is encountered.

```go
package main

import "fmt"

func main() {
  for i:=1; i<=5; i++ { // 1 2
    if i == 3 {
      break
    }
    fmt.Printf("%d ", i)
  }
}
```

### 8.7. continue

- `continue` skips the current iteration of the loop.

```go
package main

import "fmt"

func main() {
  for i:=1; i<=5; i++ { // 1 2 4 5
    if i == 3 { // skips 3
      continue
    }
    fmt.Printf("%d ", i)
  }
}
```

### 8.8. goto

- `goto` allows unconditional jump to a labelled statement **within the same function**.

```go
package main

import "fmt"

func main() {
  walk()
  // First step
  // Third step
}

func walk() {
  fmt.Println("First step")

  goto LASTSTEP

  fmt.Println("Second step") // unreachable code

  LASTSTEP:
    fmt.Println("Third step")
}
```

### 8.9. fallthrough

- `fallthrough` is used in `switch`.
- It transfers the program control just after the statement is executed in the switch cases even if the expression does not match.
- Don't put `fallthrough` in the last statement.

```go
package main
  
import "fmt"

func main() {
  switch day := "T"; day {
    case "M":
      fmt.Println("Monday")
      fallthrough
    case "T":
      fmt.Println("Tuesday") // Tuesday
      fallthrough
    case "W":
      fmt.Println("Wednesday") // Wednesday
    }
}
```

---

## 9. Concurrency

- Concurrency is the ability to handle multiple tasks simultaneously to improve performance and responsiveness.
- Goroutines and channels support communicating sequential processes, in which values are passed between independent activities (goroutines) and variables for most of the part confined to a single activity.
- If goroutines are the activities of a concurrent program, channels are the connections between them.

### 9.1. Goroutines

- Goroutine is the way of doing tasks concurrently in Go. It is a lightweight thread managed by the Go runtime.
- It exists only in the virtual space of the Go runtime, not in the OS.
- Go Runtime scheduler manages its lifecycle. OS sees a single user-level process requesting and running multiple threads.
- The main goroutine should be running for any other goroutines to run. If the main goroutine terminates then the program will be terminated and no other goroutine will run.
- Goroutines run in the same address space so access to shared memory must be synchronized.
- When a new goroutine is started, the goroutine call returns immediately. Unlike functions, the control does not wait for the goroutine to finish executing. The control returns immediately to the next line of code after the goroutine call and any return values from the goroutine are ignored.

- `go <method_or_function_name>()` creates a new goroutine that calls the given function or method, and doesn't wait.

```go
go f(x, y, z) // starts a new goroutine running `f(x, y, z)`
// f, x, y, and z are evaluated in the current goroutine.
// f is executed in the new goroutine.
```

- When a program starts, only the _main goroutine_ will be called.

```go
/* Output:
  1-cat: Alba
  2-cat: Ana
  1-flower: Calafate
  3-cat: Angelina
  2-flower: Canelo
  Time is up!
 */

package main

import (  
    "fmt"
    "time"
)

func cat_names() {
    cats := [3]string{"Alba", "Ana", "Angelina"}
    for i, c := range cats {
        time.Sleep(2 * time.Millisecond)
        fmt.Printf("%d-cat: %s\n", i+1, c)
    }
}

func flower_names() {  
    flowers := [3]string{"Calafate", "Canelo", "Chauchau"}
    for i, f := range flowers {
        time.Sleep(5 * time.Millisecond)
        fmt.Printf("%d-flower: %s\n", i+1, f)
    }
}

func main() {  
    go cat_names()
    go flower_names()
    time.Sleep(11 * time.Millisecond)
    fmt.Println("Time is up!") // Chauchau cannot be printed!
}
```

### 9.2. Channels

- Channels are the pipes that connect concurrent goroutines.
- Each channel is a conduit for values of a particular type, called the channel's element type. It is a reference to the data structure created by `make`.
  - `ch := make(chan int)` // ch has type 'chan int'
- `==` compares two channels of the same type.
- Basic operations of channels:
  - `send` sends the data to the channel, `<channel_name> <- <data>`.
  - `receive` receives the data from the channel, `<- <channel_name>`.
  - `close`
  - A `send` always happens before a `receive`.
- Channels let concurrent processes synchronize by sending messages to each other instead of sharing memory.

```go
ch <- a // send transmits a value from goroutine to another

a = <-ch // receive gets the value to another goroutine executing a corresponding receive expression
<-ch // receive where the result is discarded.

// close
close(ch) // sets a flag indicating that no more values will ever be sent on this channel and subsequent attempts to send will panic.
```

#### 9.2.1. Unbuffered channels

- By default, channels are unbuffered.
- It is a channel that cannot initially store messages inside it.
- You need to fill in the message to make the goroutine process unblocked by the channel.
- It ensures that communication between goroutines is synchronized and that data is transferred reliably.

```go
package main

import (
 "fmt"
)

func assign_x(ch chan int) {
 x := 1
 ch <- x // send x on the channel
}

func main() {
 ch := make(chan int) // create the channel
 defer close(ch) // close the channel at the end

 go assign_x(ch)

 x := <-ch // receive x from the channel
 fmt.Printf("x = %d\n", x)
}
```

#### 9.2.2. Buffered channels

- Channels can be buffered.
- A buffered channel is created with `make`, and its capacity is nonzero.
- It accepts a limited number of values without a corresponding receiver for those values.
- It only blocks the sending goroutine in case the buffer is full.

```go
package main

import "fmt"

func main() {
  /* Output := 
     hello
     world
   */
    messages := make(chan string, 2)
    messages <- "hello"
    messages <- "world"
    fmt.Println(<-messages)
    fmt.Println(<-messages)
}
```

- `WaitGroup` waits for multiple goroutines to finish. It should be passed into functions by a pointer if it is done explicitly.

#### 9.2.3. select

- It executes a channel among many alternatives.

```go
package main

import (
  "fmt"
)

func main() {
  select {
    case firstChannel:
    case secondChannel:
    case thirdChannel:
  }
}
```

- For more [details](https://www.programiz.com/golang/select).

---

## 10. Memory management

### 10.1. Memory allocation

- Memory allocation and deallocation happen automatically.
- Autonomous implementation of memory usage patterns such as memory pooling, preallocation, etc. avoids making a system call for each memory allocation.
- Whether an object will be stack or heap allocated is decided by the compiler.

#### 10.1.1. `new()` and `make()`

- Both will allocate and get a memory address.
- `new()` is not initialized. It is so you cannot put any data initially.
- `make()` is more common. It is initialized and non-zeroed storage so you can put data initially.

### 10.2. Garbage collection (GC)

- It happens automatically.
- It allows automatic memory management to make code cleaner and avoid memory leaks.
- Out of scope or `nil`

---

## 11. Clockwise/Spiral rule

It is a technique to parse any `C` declaration. There are three steps:

1. Starting with the unknown element, move in a spiral/clockwise direction; when encountering the following replace them with the corresponding English statements:

   - `[X]` or `[]` => Array `X` size of ... or Array undefined size of ...
   - `(type1, type2)` => function passing `type1` and `type2` returning ...
   - `*` => pointer(s) to ...

2. Keep doing this in a spiral/clockwise direction until all tokens are covered.

3. Always resolve anything in parentheses first!

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
