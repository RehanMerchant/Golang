# Getting Started

![image](https://quotefancy.com/media/wallpaper/3840x2160/8151353-Hello-World-Wallpaper.jpg)

It is mandatory for all programer to get started with a language with a **Hello world** program, lets write your first program in go and understand the least of go.

Create a file called `main.go` in any directory you like and write the program below.

```
package main

 import "fmt"

 func main() {
   fmt.Println("Hello world!") // Hello world!
}
```

Open a terminal in that directory and write `go run main.go`, You will see Hello world! What is does when we run the go run main.go commnd it takes the raw file and compile it to make an executable file store somewhere in a temp folder (depends on the operating system), executes it and finally shows us our output.

We could create the executable file in the same directory using `go build` command.
Run `go build main.go`, you will see an executable file will be their with the name of main (the file name), However you can change your executable file name using this command `go build -o hello_world main.go`, it will create a file called hello_world

you can run the executable file `./hello_world` or `./main` based on your file name.

### Packages and Imports

[Read original Post](https://www.geeksforgeeks.org/go-language/packages-in-golang/)

Packages are the most powerful part of the Go language. The purpose of a package is to design and maintain a large number of programs by grouping related features together into single units so that they can be easy to maintain and understand and independent of the other package programs.
This modularity allows them to share and reuse. In Go language, every package is defined with a different name and that name is close to their functionality like "strings" package and it contains methods and functions that only related to strings.

`main` package is a special package that contain the main function, which serves as the entry point of the excutable go program.

1. Import paths: In Go language, every package is defined by a unique string and this string is known as import path. With the help of an import path, you can import packages in your program. For example:

```
import "fmt"
```

This statement states that you are importing an fmt package in your program. The import path of packages is globally unique. To avoid conflict between the path of the packages other than the standard library, the package path should start with the internet domain name of the organization that owns or host the package. For example:

```
import "geeksforgeeks.com/example/strings"
```

2. Package Declaration: In Go language, package declaration is always present at the beginning of the source file and the purpose of this declaration is to determine the default identifier for that package when it is imported by another package. For example:

```
package main
```

3. Import declaration: The import declaration immediately comes after the package declaration. The Go source file contains zero or more import declaration and each import declaration specifies the path of one or more packages in the parentheses. For example:

```
// Importing single package
import "fmt"

// Importing multiple packages
import(
"fmt"
"strings"
"bytes"
)
```

4. Blank import: In Go programming, sometimes we import some packages in our program, but we do not use them in our program. When you run such types of programs that contain unused packages, then the compiler will give an error. So, to avoid this error, we use a blank identifier before the name of the package. For example:

```
import _ "strings"
```

It is known as blank import. It is used in many or some occasions when the main program can enable the optional features provided by the blank importing additional packages at the compile-time.

5. Nested Packages: In Go language, you are allowed to create a package inside another package simply by creating a subdirectory. And the nested package can import just like the root package. For example:

```
import "math/cmplx"
```

Sometimes some packages may have the same names, but the path of such type of packages is always different. For example, both math and crypto packages contain a rand named package, but the path of this package is different, i.e, math/rand and crypto/rand.

**Naming convection for packages**

In Go language, when you name a package you must always follow the following points:

- When you create a package the name of the package must be short and simple. For example strings, time, flag, etc. are standard library package.
- The package name should be descriptive and unambiguous.
- Always try to avoid choosing names that are commonly used or used for local relative variables.
- The name of the package generally in the singular form. Sometimes some packages named in plural form like strings, bytes, buffers, etc. Because to avoid conflicts with the keywords.

### Data Types

Resources:
[Youtube: Data Types](https://www.youtube.com/watch?v=WFbiye5eUyw&list=PLq3etM-zISamTauFTO5-G5dqBN07ckzTk&index=2),
[Youtube: Integer](https://www.youtube.com/watch?v=SrKayqonHos&list=PLq3etM-zISamTauFTO5-G5dqBN07ckzTk&index=3),
[Youtube: Float and Complex](https://www.youtube.com/watch?v=Bb_K7SEq_wk&list=PLq3etM-zISamTauFTO5-G5dqBN07ckzTk&index=4),
[Youtube: String](https://www.youtube.com/watch?v=6xUyifHmgWA&list=PLq3etM-zISamTauFTO5-G5dqBN07ckzTk&index=5)

Data type is an important concept in programming. Data type specifies the size and type of variable values. Go is statically typed, meaning that once a variable type is defined, it can only store data of that type.

There are majorly three basic data types (Primitive Data types)

- Boolean (true and false)
- Numerics (Integer, flotaing and compex numbers)
- String (words, sentence)

All the data types have a Zero value (Default value) like for bool it is false, for string it is `""` (Empty string) and the Numerics section is very vast, it contain types of natural number, decimal, complex and imaginary number so there is no zero type for the group Numerics. We will discuss about each primitive type further.

```
package main

import "fmt"

func main() {

	var str string   // str variable is of string type
	fmt.Println(str) // Zero value of string is "" (empty string)
	str = "Hello"    // Initializing "Hello" to str
	fmt.Println(str) // Hello

	var num int      // num variable is of int type
	fmt.Println(num) // Zero value of int is 0
	num = 10         // Initializing 0 to num
	fmt.Println(num) // Hello

	var isbool bool     // isbool variable is of bool type
	fmt.Println(isbool) // Zero value of bool is false
	isbool = true       // Initializing true to isbool
	fmt.Println(isbool) // true

}
```

#### Numerics

Numerics are just number that can be 1, 230, -45, 12.23, 32i. Anything we can count, but there are different types of numerics, Lets discuss about each numeric data type in detail

**Integers (int)**

The int data type is used to store positive and negative integers (without fractions), Yet there are different types of int in go `int8`, `int16`,`int32`, `int64`, `uint8`, `uint16`,`uint32`, `uint64` and finally `int`, `uint`. All these data types have different sizes in memory and ranges

The `u` infont of int suggest that they are unsinged that means it starts from 0 and contain only positive number

The size in memory of the data types is 8 in case of int8 or uint8 and likewise. 1 Byte = 8 bit the numbers at the end represents memory in bits int16/uint16 is 2 Byte. In memory the first bit is always used to store the sing of the value and rest all to store the vlaue.

| Type       | Range                                                   |
| ---------- | ------------------------------------------------------- |
| int8       | -128 to 127                                             |
| int16      | -32768 to 32767                                         |
| int32      | -2,147,483,648 to 2,147,483,647                         |
| int64      | -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807 |
| uint8/byte | 0 to 255                                                |
| uint16     | 0 to 65,535                                             |
| uint32     | 0 to 4,294,967,295                                      |
| uint64     | 0 to 18,446,744,073,709,551,615                         |

All the types listed above are distinct types in go, noting can be compared with others than itself.

`int` and `uint` are just alias to `int32 or int64` and `uint32 and uint64` respectively. It can be either int/uint 32 or int/uint64 based on your system architecture.

`uint8` is alias to byte, uint8 is 8 bit which is 1 Byte and the range is from 0 to 255 same as byte

`int32` is alias to rune (we will discuss about it further)

```
package main

import "fmt"

func main() {

var myuint8 uint8
myuint8 = 10 // it should not exceed 255 otherwise will cause overflow error
fmt.Println(myuint8)

var myint8 uint8
myuint8 = -40 // it should not exceed 127 and cant go below -128
fmt.Println(myint8)

// Try all other datatypes by yourself

}
```

**Float and Complex Types**

Floating point numbers have integer value, a decimal point and a fraction value. Go used `IEEE 754` standard to implement floats, example: 35.3, -2.34, or 3597.34987.

Floats too have sub-types like `float32` `float64` which has differnet range and memory space. float64 is the default data type for float.
float64 has high precision than float32.

| Type    | Range                |
| ------- | -------------------- |
| float32 | -3.4e+38 to 3.4e+38. |
| float64 | -3.4e+38 to 3.4e+38. |

Complex numbers are the extentions of float. There are 2 types of Complex types `complex32` and `complex 64`.

Complex number in go have the real and imaginary parts represented by float, complex64 used float32 for real and imaginary part each while complex128 used float64 as the real and imaginary part each.

There is a built-in function `complex()` which is used to create complex number. `real()`, `imag()` are the function to get real and imaginary parts of the compex number

```
package main

import "fmt"

func main() {
	var myfloat32 float32
	fmt.Println(myfloat32) // 0.0
	myfloat32 = 123.12324
	fmt.Println(myfloat32)

	var myfloat64 float64
	fmt.Println(myfloat64)
	myfloat64 = 1232.1232435353
	fmt.Println(myfloat64)

  myfloat64 = 23.242315423153125325325
  fmt.Println(myfloat64) // 23.2423154231531253253 (it will be truncated because of overflow)
}

```

You should always use floats carefully ,You should avoid direct equality comparisons with floats, In loops or aggregations small rounding errors may happen. it may truncate the values if overflow happens.

```
package main

import "fmt"

func main() {

	var mycomplex complex128
	mycomplex = complex(23.43545423535, 22.242413253253)
	fmt.Println(mycomplex)

  var realpart, imaginarypart float64 // float64 cause we are going to extract from a complex128

  realpart = real(mycomplex)
  imaginarypart = imag(mycomplex)

  fmt.Println(realpart,imaginarypart)

}

```

Try all explained feature of your own to get a better understanding of the fundamentals of go.

#### Boolean (bool)

bool data type represents either true or false, These values are fundamental for controlling flow through conditional and logical statements.

The memory size of bool in go is 1 Byte and zero value of bool is false.

```
package main

import "fmt"

func main() {

	var isbool bool     // isbool variable is of bool type
	fmt.Println(isbool) // Zero value of bool is false
	isbool = true       // Initializing true to isbool
	fmt.Println(isbool) // true

}
```

#### Strings

String data types are used for text in go, we can define string with only `""` double quotes and backticks, Example: "Hello world". Empty string is the zero value for string. Go supports **Unicode**, it is the reason we can use various character and symbols and emojis.

Unicode has a number/code representation for symbols, characters and emojis from multiple languages around the world. The number represent the specific characters enable us to use tons of characters.

Strings are stored as byte array in go which are immutable. Strings are made up of rune(int32), which is the perfect representation of a character in go because of UTF-8 encoding where each character can take 1 to 4 Bytes in memory

There are lots of in-built functions to format strings. The fmt, strings package will come in handy, which we will discuss ahead

```
package main

import "fmt"

func main() {

  var str string
  fmt.Println(str)
  str = "Hello"
  fmt.Println(str)

  var str2 string
  fmt.Println(str2)
  str2 = "World"
  fmt.Println(str)

  fmt.Println(str + " " + str2)
  fmt.Printf("%s %s\n",str,str2)

//Explore all other functions of ftm of your own

}
```

You can check the data type of the variable using fmt in go, There are lots of other things about fmt we will talk further but here is an simple example:

```
age := 12.22
fmt.Printf("Type of age is: %T\n", age)  // Output: float64
```

### Variable and Constants

Resources:
[Youtube: Variable](https://www.youtube.com/watch?v=UN5wEcW2I1o&list=PLq3etM-zISamTauFTO5-G5dqBN07ckzTk&index=6),
[Youtube: Constanst](https://www.youtube.com/watch?v=wxhgWXfXUb8&list=PLq3etM-zISamTauFTO5-G5dqBN07ckzTk&index=7),

Variables are used to store values, that will be used in further program and that variable can be changed throught the program, There are scope of variables, like if variable are declared in **Package level** that can be used and changed throught the whole package and there is **Function level** variable which are only allowed to use inside the respective function.

Declared/Initilized variable which is unused in the program will cause a compile time error. It is mandatory to use all variables.

```
package main

import "fmt"

var myint int = 10 //package level declaration

func main() {
var myfloat float64 = 44.55
smt() // calling smt function that prints 12.43 not 44.55

}

func smt(){
	var myfloat float64 = 12.43 // function level declaration cand be used only inside the scopr of smt function
	fmt.Println(myfloat)
}
```

Each variable must have a type associated to it, There are two ways to declare variable **Explicit** and **Implicit**

```
var name string  //variable named 'name' which is a type of string
var age int = 19; // age named variable with 10 stored in it
```

The above example is the type of explicit declaration where the programmer has to create a variable with its type. Initially the variable will contain the zero value of the data type.

Implict declaration, when a variable infered the data type of its own, this can be done using short variable declaration.

```
age := 19 //Implicit declaration of variable age to 19
```

In the above example, we can see we dont have to use var and instead of = we use := , Here age variable automatically infer the type based on the value, here it is int cause 19 fallthrough under int category.

19 also comes under int8,16,32,64 and uint8,16,32,64 why int is choosed as the type of the variable, It is because go generally decides to infer to the default type and Using int8, int16, etc, can lead to extra CPU instructions for sign extension and type conversion, which can slow down performance, Since CPUs are optimized for their native word size, using int allows the Go compiler to generate faster machine code on most platforms.

```
age:=19 //int
money:=12.44 //float64
name:="Rehan" //string
```

**Multiple variable declaration**

```
a, b, c := 10, 20, 30
name, age := "Rehan", 19

var x, y int = 1, 2
var name, isStudent = "Rehan", true

var a, b, c int     // all are 0 by default
var s1, s2 string   // all are "" by default

var (
    name     = "Rehan"
    age      = 22
    isActive = true
)

var (
    x int
    y string
    z bool
)

// Try it out of your self
```

**Constants**

Constants are values that once initialized can't be changed during the execution of the program (immutable). It is declared using `const` keyword like `var` for declaring variable. It is evaluated at compile time and it can be used anywhere a literal could be used.

Boolean (true,false), Numeric (1,100,12.33,-23), String ("Hello") and Rune('A', 'ई') can be stored as constant in go.

There are two types of constanst: **typed** and **untyped**. Typed constanst has a type associated with it like int,bool etc. and untyped constanst, were the value is automitically infered or it fallbakc to default type for the constant value.

Constanst can be declared and initilized in Package or function level like variable, they cna also be grouped using parenthesis.

Unlike variable there can be unused constants.

```
const name = "Rehan"
const age = 22
const pi = 3.14

const x = 10    // untyped

const y int = 10  // typed constant

//multiple
const (
    A = 1
    B = 2
    C = 3
)

const x = 10 + 5
const y = x * 2
```

**Iota**

Iota is a special feature in go that is used to generate constants for enumerated constants. iota is a predeclared identifier in Go used inside const blocks to generate sequential values automatically.

It’s often used to create enums, flags, and bit patterns.

Iota always starts with 0 for the first ocnstants in a block and it is incremented by 1 for each line.

```
const (
    A = iota  // 0
    B         // 1
    C         // 2
)

fmt.Println(A, B, C) // 0 1 2

const (
    D = iota + 1  // 1
    E             // 2
    F             // 3
)

fmt.Println(D, E, F) // 1 2 3
```

### Identifiers and Keyword

Identifiers are the names we assing to the variable,constanst, functions, types, labels and packages for the use of the programmer to point to the information stored in memory while writing programs.

There are certain rules that are to be followed while naming a identifier

- Must begin with a letter (A-Z or a-z) or underscore (\_)
- Can contain letters, digits, and underscores.
- Cannot begin with a digit.
- Cannot use predeclared identifiers as identifiers.

Predeclared identifiers are as follows:
`any`,`bool`,`byte`,`comparable`,`compex64`,`complex128` and all other **Types**.
`true`,`false`,`iota`,`nil` and other predeclared functions name like `real()`,`len()` etc.

**Keywords**

Keywords are reserved words that have special meaning in the Go language syntax.
You cannot use them as identifiers (variable names, function names, etc.).

There are list of 25 keywords

```
break       default     func        interface   select
case        defer       go          map         struct
chan        else        goto        package     switch
const       fallthrough if          range       type
continue    for         import      return      var
```

Try coding all the things stated here weather it is true or not.

### Operator

[Read original Blog](https://www.geeksforgeeks.org/go-language/go-operators/)

Operators allow us to perform different kinds of operations on operands like additions, multiplication etc. There are various kinds of operator which we will be discussing throughly ahead.

Operator combine operands into expression

`2 + 2` Here 2,2 are the operands and `+` is the operator, the operator is peforming task on operands to make it an expression

Binary operator peforms operations on two operands while unary operator peforms on single operand. `++`,`--`,`!`,`*`,`&` etc are the example of unary operator and `/`,`*` etc are the example of binary operator.

Lets go through all kinds of operator and learn its uses and function.

**Arithmetic Operator**

These are used to perform arithmetic/mathematical operations on operands in Go language

| Operator | Operation  |
| -------- | ---------- |
| +        | Sum        |
| -        | Difference |
| \*       | Product    |
| /        | Division   |
| %        | Reminder   |

```
// Go program to illustrate the
// use of arithmetic operators
package main

import "fmt"

func main() {
   p:= 34
   q:= 20

   // Addition
   result1:= p + q // Integers, floats, complex values and string (concatination)
   fmt.Printf("Result of p + q = %d", result1)

   // Subtraction
   result2:= p - q // Integers, floats and complex values
   fmt.Printf("\nResult of p - q = %d", result2)

   // Multiplication
   result3:= p * q  // Integers, floats and complex values
   fmt.Printf("\nResult of p * q = %d", result3)

   // Division
   result4:= p / q  // Integers, floats and complex values
   fmt.Printf("\nResult of p / q = %d", result4)

   // Modulus
   result5:= p % q  // Integers
   fmt.Printf("\nResult of p %% q = %d", result5)
}
```

**Output:**

```
Result of p + q = 54
Result of p - q = 14
Result of p * q = 680
Result of p / q = 1
Result of p % q = 14
```

**Relational Operator**

Relational operators are used for the comparison of two values and it returns the result in boolean types

| Operator | Operation            |
| -------- | -------------------- |
| ==       | Equal to             |
| !=       | Not equal to         |
| >        | Greter than          |
| <        | Less than            |
| >=       | Greter than equal to |
| <=       | Less than equal to   |

```
// Go program to illustrate the
// use of relational operators
package main

import "fmt"

func main() {
   p:= 34
   q:= 20

   // ‘=='(Equal To)
   result1:= p == q
   fmt.Println(result1)

   // ‘!='(Not Equal To)
   result2:= p != q
   fmt.Println(result2)

   // ‘<‘(Less Than)
   result3:= p < q
   fmt.Println(result3)

   // ‘>'(Greater Than)
   result4:= p > q
   fmt.Println(result4)

   // ‘>='(Greater Than Equal To)
   result5:= p >= q
   fmt.Println(result5)

   // ‘<='(Less Than Equal To)
   result6:= p <= q
   fmt.Println(result6)


}
```

**Output:**

```
false
true
false
true
true
false
```

**Logical Operator**

They are used to combine two or more conditions/constraints or to complement the evaluation of the original condition in consideration. They are typically used in conditions (if, for, etc.).

| Operator | Operation |
| -------- | --------- |
| &&       | AND       |
| ｜｜     | OR        |
| !        | Not       |

```
// Go program to illustrate the
// use of logical operators
package main
import "fmt"
func main() {
    var p int = 23
    var q int = 60

    if(p!=q && p<=q){
        fmt.Println("True")
    }

    if(p!=q || p<=q){
        fmt.Println("True")
    }

    if(!(p==q)){
        fmt.Println("True")
    }

}
```

**Output:**

```
True
True
True
```

**Bitwise Operator**

Bitwise operator are kind of operator which works at bit level and used to peform bit by bit operations mainly used for binary (0 & 1) operations only work on integer data type.

| Operator | Operation         |
| -------- | ----------------- |
| &        | Bitwise AND       |
| ｜       | Bitwise OR        |
| ^        | Bitwise XOR       |
| &^       | Bit clear AND NOT |
| <<       | Left Shift        |
| >>       | Right SHift       |

- `&` (bitwise AND): Takes two numbers as operands and does AND on every bit of two numbers. The result of AND is 1 only if both bits are 1.
- `|` (bitwise OR): Takes two numbers as operands and does OR on every bit of two numbers. The result of OR is 1 any of the two bits is 1.
- `^` (bitwise XOR): Takes two numbers as operands and does XOR on every bit of two numbers. The result of XOR is 1 if the two bits are different.
- `<<` (left shift): Takes two numbers, left shifts the bits of the first operand, the second operand decides the number of places to shift.
- `>>` (right shift): Takes two numbers, right shifts the bits of the first operand, the second operand decides the number of places to shift.
- `&^` (AND NOT): This is a bit clear operator.

```
// Go program to illustrate the
// use of bitwise operators
package main

import "fmt"

func main() {
   p:= 34
   q:= 20

   // & (bitwise AND)
   result1:= p & q
   fmt.Printf("Result of p & q = %d", result1)

   // | (bitwise OR)
   result2:= p | q
   fmt.Printf("\nResult of p | q = %d", result2)

   // ^ (bitwise XOR)
   result3:= p ^ q
   fmt.Printf("\nResult of p ^ q = %d", result3)

   // << (left shift)
   result4:= p << 1
   fmt.Printf("\nResult of p << 1 = %d", result4)

   // >> (right shift)
   result5:= p >> 1
   fmt.Printf("\nResult of p >> 1 = %d", result5)

   // &^ (AND NOT)
   result6:= p &^ q
   fmt.Printf("\nResult of p &^ q = %d", result6)

    }
```

**Output:**

```
Result of p & q = 0
Result of p | q = 54
Result of p ^ q = 54
Result of p << 1 = 68
Result of p >> 1 = 17
Result of p &^ q = 34
```

Let us understand what happened in the above example

- p = 34, in binary: 00100010
- q = 20, in binary: 00010100

**`p & q` Bitwise And**

```
  00100010  (34)
& 00010100  (20)
----------
  00000000  → 0
```

Bitwise AND returns 1 only if both bits are 1. Since there is no position where both p and q have 1, the result is 0.

**`p | q` Bitwise OR**

```
  00100010  (34)
| 00010100  (20)
----------
  00110110  → 54
```

Bitwise OR returns 1 if either bit is 1. Combining bits sets all 1s from both numbers → result is 54

**`p ^ q` Bitwise XOR**

```
  00100010  (34)
^ 00010100  (20)
----------
  00110110  → 54

```

Bitwise XOR returns 1 only if the bits are different. That's why result is again 54 here.

**`p << 1` Left Shift**

```
00100010 << 1 → 01000100
```

Left shift moves all bits one place to the left, adding a 0 at the right end:

Binary 01000100 = 68

**`p >> 1` Right Shift**

```
00100010 >> 1 → 00010001
```

Right shift moves all bits one place to the right, discarding the rightmost bit:

Binary 00010001 = 17

**`p &^ q` Bit Clear (AND NOT)**

```
00100010  (34)
&^
00010100  (20)
----------
00100010 & (^00010100)
        = 00100010 & 11101011
        = 00100010 → 34
```

&^ means "AND NOT". It clears the bits in p where q has 1s. Since q doesn't share any 1 bits with p, p remains unchanged → 34.

You can read more about it from [here](https://dzone.com/articles/bitwise-operators-in-go)

**Assignment Operators**

Assignment operators are used to assigning a value to a variable. The left side operand of the assignment operator is a variable and right side operand of the assignment operator is a value.
`=` is the simple exmple of assingment operator but will will explore other types of assingment operator as well

- `= (Simple Assignment)`: This is the simplest assignment operator. This operator is used to assign the value on the right to the variable on the left.
- `+= (Add Assignment)`: This operator is a combination of ‘+’ and ‘=’ operators. This operator first adds the current value of the variable on left to the value on the right and then assigns the result to the variable on the left.
- `-= (Subtract Assignment)`: This operator is a combination of ‘-‘ and ‘=’ operators. This operator first subtracts the current value of the variable on left from the value on the right and then assigns the result to the variable on the left.
- `*= (Multiply Assignment)`: This operator is a combination of ‘\*’ and ‘=’ operators. This operator first multiplies the current value of the variable on left to the value on the right and then assigns the result to the variable on the left.
- `/= (Division Assignment)`: This operator is a combination of ‘/’ and ‘=’ operators. This operator first divides the current value of the variable on left by the value on the right and then assigns the result to the variable on the left.
- `%= (Modulus Assignment)`: This operator is a combination of ‘%’ and ‘=’ operators. This operator first modulo the current value of the variable on left by the value on the right and then assigns the result to the variable on the left.
- `&= (Bitwise AND Assignment)`: This operator is a combination of ‘&’ and ‘=’ operators. This operator first “Bitwise AND” the current value of the variable on the left by the value on the right and then assigns the result to the variable on the left.
- `^= (Bitwise Exclusive OR)`: This operator is a combination of ‘^’ and ‘=’ operators. This operator first “Bitwise Exclusive OR” the current value of the variable on left by the value on the right and then assigns the result to the variable on the left.
- `|= (Bitwise Inclusive OR) `: This operator is a combination of ‘|’ and ‘=’ operators. This operator first “Bitwise Inclusive OR” the current value of the variable on left by the value on the right and then assigns the result to the variable on the left.
- `<<= (Left shift AND assignment operator)`: This operator is a combination of ‘<<’ and ‘=’ operators. This operator first “Left shift AND” the current value of the variable on left by the value on the right and then assigns the result to the variable on the left.
- `>>= (Right shift AND assignment operator)`: This operator is a combination of ‘>>’ and ‘=’ operators. This operator first “Right shift AND” the current value of the variable on left by the value on the right and then assigns the result to the variable on the left.

```
// Go program to illustrate the
// use of assignment operators
package main

import "fmt"

func main() {
   var p int = 45
    var q int = 50

   // “=”(Simple Assignment)
   p = q
   fmt.Println(p)

   // “+=”(Add Assignment)
    p += q
   fmt.Println(p)

   //“-=”(Subtract Assignment)
   p-=q
   fmt.Println(p)

   // “*=”(Multiply Assignment)
   p*= q
   fmt.Println(p)

   // “/=”(Division Assignment)
    p /= q
   fmt.Println(p)

    // “%=”(Modulus Assignment)
    p %= q
   fmt.Println(p)

}
```

**Output:**

```
50
100
50
2500
50
0
```

There are some other kind of operator, listed below

| Operator | Operation        |
| -------- | ---------------- |
| ++       | Increment        |
| --       | Decrement        |
| &        | Address          |
| \*       | De-redrefrencing |
| <-       | Channel          |

`++` Operator used to increse the value by one like `var a int = 10` `a++ // it will increase the value to 11`.

`--` Operator decreses the value by one.

We will be discussing about Address, De-refrencing and Channel operator ahead.

**Operator Precedence**

The precedence of operator is followed by `PEMDAS` where `P` is Parenthesis, `E` is Exponents, `M` for Multiplication, `D` for Division `A` for Addition and `S` is Substraction.

There are other operator precedence that should be considered

| Precendence | Operator             |
| ----------- | -------------------- | --- |
| 6           | ++, --               |
| 5           | \*,/,%,<<,>>,&,&^    |
| 4           | +, -,                | , ^ |
| 3           | ==, !=, <, >, <=, >= |
| 2           | &&                   |
| 1           | ｜｜                 |

\*_6 is the highest precedence and 1 is lowest and all are evluated from left to right_
