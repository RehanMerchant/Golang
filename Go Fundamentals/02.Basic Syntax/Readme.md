# Getting Started

![image](https://quotefancy.com/media/wallpaper/3840x2160/8151353-Hello-World-Wallpaper.jpg)

It is mandatory for all programer to get started with a language with a **Hello world** program, lets write your first program in go and understand the least of go.

Create a file called ``main.go`` in any directory you like and write the program below.

```
package main

 import "fmt"

 func main() {
   fmt.Println("Hello world!") // Hello world!
}
```

Open a terminal in that directory and write ``go run main.go``, You will see Hello world! What is does when we run the go run main.go commnd it takes the raw file and compile it to make an executable file store somewhere in a temp folder (depends on the operating system), executes it and finally shows us our output.

We could create the executable file in the same directory using ``go build`` command.
Run ``go build main.go``, you will see an executable file will be their with the name of main (the file name), However you can change your executable file name using this command ``go build -o hello_world main.go``, it will create a file called hello_world

you can run the executable file ``./hello_world`` or ``./main`` based on your file name.

### Packages and Imports

[Read original Post](https://www.geeksforgeeks.org/go-language/packages-in-golang/)

Packages are the most powerful part of the Go language. The purpose of a package is to design and maintain a large number of programs by grouping related features together into single units so that they can be easy to maintain and understand and independent of the other package programs.
This modularity allows them to share and reuse. In Go language, every package is defined with a different name and that name is close to their functionality like "strings" package and it contains methods and functions that only related to strings.

``main`` package is a special package that contain the main function, which serves as the entry point of the excutable go program.

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

The size in memory of the data types is 8 in case of int8 or uint8 and likewise. 1 Byte = 8 bit the numbers at the end represents memory in bits int16/uint16 is 2 Byte.  In memory the first bit is always used to store the sing of the value and rest all to store the vlaue.

| Type    | Range |
| -------- | ------- |
| int8  | -128 to 127    |
| int16 | -32768 to 32767   |
| int32    |  -2,147,483,648 to 2,147,483,647    |
| int64    |  -9,223,372,036,854,775,808 to 9,223,372,036,854,775,807    |
| uint8/byte  |  0 to 255    |
| uint16 | 0 to 65,535   |
| uint32    |  0 to 4,294,967,295    |
| uint64    |  0 to 18,446,744,073,709,551,615    |

All the types listed above are distinct types in go, noting can be compared with others than itself.

`int`  and  `uint` are just alias to `int32 or int64` and `uint32 and uint64` respectively. It can be either int/uint 32 or int/uint64 based on your system architecture.

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

| Type    | Range |
| -------- | ------- |
| float32  | -3.4e+38 to 3.4e+38.   |
| float64 | -3.4e+38 to 3.4e+38.   |

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


**Strings**

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