# Complex Types

![image](https://blogs.opentext.com/wp-content/uploads/2019/10/Complex_Data_Types_276089667-2160cropped.jpg)

In Go, complex types go beyond the basic data types to allow developers to work with more structured, flexible, and powerful data representations. These include arrays, slices, maps, structs, and interfaces—each designed to handle different use-cases such as collections, dynamic data, or custom models. Mastery of these complex types is essential for writing idiomatic and efficient Go code, enabling better data organization, manipulation, and real-world problem solving.

These complex types are widely used in real-world Go programs:

- Arrays and Slices are essential for storing and processing sequences of data like a list of user names, sensor readings, or request logs. Slices, in particular, are dynamic and more commonly used due to their flexibility.

- Maps allow you to create key-value pairs, making them ideal for use cases like counting word frequencies, storing configuration values, or caching responses.

- Structs help group related data into a single custom type. For example, a User struct might contain fields like Name, Email, and Age, making data more meaningful and easier to manage.

- Interfaces let you define behavior without tying your code to a specific implementation. This enables polymorphism and allows writing more modular, testable, and extensible code.

By using these complex types effectively,developers can build everything from web servers and APIs to real-time data processing systems and microservices.

Let's `range` through each complex type and explore it in depth.

### Arrays

Resources: [Blog: Array](https://www.w3schools.com/go/go_arrays.php) ,[Youtube: Array](https://www.youtube.com/watch?v=26-jj53acfg&list=PLq3etM-zISamTauFTO5-G5dqBN07ckzTk&index=17)

Arrays are used to store multiple values of the same type in a single variable, instead of declaring separate variables for each value.

- All the data stored in an array are in a contiguous block of memory
- Each piece of data stored in am array is called the element
- each element in an array are assinged with a index specifying its position
- All array start with index 0

Lets see how are Arrays stored in memory

```
    0        1       2       3       4      <- Index
 _________________________________________
|   10   |  12   |   22   |   2   |  5   |  <- Element
|________|_______|________|_______|______|


```

In the above diagram we cann see a continious block of element storing int datatype value with each element having address as index. The length of array is 5.

Suppose the above array is named as `arr` we can access the first element by using `arr[0]` this will give the value of the element in that position `10`. and we can get all its respevtively value till `arr[4]` if we try to extract the value from the position beyond 4 the code panics

`var array_name = [length]datatype{values}`, This is the syntax for declaring a array with a specified length and it is mandatory to give information about size when we are declaring an array.

```
package main
import ("fmt")

func main() {
  var arr1 = [3]int{1,2,3}
  arr2 := [5]int{4,5,6,7,8}
  arr3 := [5]int{5,2:10,50}
  arr4 := [...]int{1,2}

  fmt.Println(arr1)
  fmt.Println(arr2)
  fmt.Println(arr3)
}
```

Output

```
[1 2 3]
[4 5 6 7 8]
[5 0 10 50 0]
[1 2]
```

Above we can see arr1 and arr2 are declared normally the only difference is that arr2 used shorthand operator (walrus operator). arr3 contain 5 elements spaces but while initlizing there are only 3 elements 5 for index 0, 10 for index 2 `2:10 means 10 for index 2` and 50 for index three. In arr4 we put `...` inside the array length bracked that signifies that we are unsure how many elements we will add, once we initilized the length will be determined till then the length will be 0, but we initilized the arr4 with value there only and we cant add more value after that.

Arrays are copmparable we can compare array with `==` operator, this returns true if the data type and the length of the both array are same, it never compare the values within it.

`len()` function provide by go is ued to get the length or the size of the array

```
len(arr4) // 2
```

**We can access all element based on its address**

```
package main
import ("fmt")

func main() {
  prices := [3]int{10,20,30}

  fmt.Println(prices[0]) //10
  fmt.Println(prices[2])  //30
}
```

**We can mutate any valid element in an array**

```
package main
import ("fmt")

func main() {
  prices := [3]int{10,20,30}

  prices[2] = 50
  fmt.Println(prices) // [10 20 50]
}
```

Like every other langauge go supports multidimensional array like 2D and 3D

```
matrix := [3][4]int{
    {1, 2, 3, 4},
    {5, 6, 7, 8},
    {9, 0, 1, 2},
} // 3 rows and 4 coloumb

fmt.Println(matrix[1][2]) // Output: 7
```

The only limitations in array is that they are of fixed size, in go there is a similar complex type with dynamic size and more features called slices so lets learn about that.

### Slices

Resources: [Blog: Slices](https://www.w3schools.com/go/go_slices.php) ,[Youtube: Slices](https://www.youtube.com/watch?v=aXl8AvawPoU&list=PLq3etM-zISamTauFTO5-G5dqBN07ckzTk&index=19)

Slices are similar to arrays, but are more powerful and flexible.
Like arrays, slices are also used to store multiple values of the same type in a single variable.
However, unlike arrays, the length of a slice can grow and shrink as you see fit.
Slices are wapper around arrays, they manage the underlying arrays and make in more flexible and featureful.

Like arrays all slices have length too witch determines the length of the slice (the number of elements stored) and there is another thing called capacity which the total capacity of elements that the array can grow or shrink
(we will understand it better when we will know about how slices work)

`cap()` function is used get the capacity of the array, for array the len and cap will be same. Whereas in slices it may or may not be same

**Important**

When we create a slices of certain length, the go compiler create the underlying array usually of double the length ( _for smaller slices and for larger grows by 25%. It is not exactly known how it work, but it create larger underlying array_ ), When we reach the capacity of the slice, it creates another larger array copying all the data to the new array. **This functionality allows slices to have append function to add more value and keeping the array dynamic**

`slice_name := []datatype{values}` This is the syntax of declaring slices, the brackets must be empty to signify slices

```
var sli []string // Declared only | len-0 cap-0
myslice1 := []int{} // len-0 cap-0
myslice2 := []int{1,2,3} //len-3 cap-3
sli:= make([]int,0)
```

In the above example we saw how we declared slices with different methods using walrus operator, using var and make function

**Make**

Make function is a inbuilt function used to create many internal things we will dicuss ahead. It is also used to create Slices, It takes a type of slice as the first as argument and length as second and capacity as third (optional)

`a:= make([]int, 5)` a is a slice of int with length 5 and capacity 5
`a:= make([]int, 5, 10)` a is a slice of int with length 5 and capacity 10

**Slices from Array**

```
package main
import ("fmt")

func main() {
  arr1 := [6]int{10, 11, 12, 13, 14,15}
  myslice := arr1[2:4]

  fmt.Printf("myslice = %v\n", myslice)
  fmt.Printf("length = %d\n", len(myslice))
  fmt.Printf("capacity = %d\n", cap(myslice))
}
```

In the above exmaple we create an array of length 6 and we create a slice over it with a notation `2:4` this wrapped with squar brackets signifies that we are creating a slice from a array or slice and that slice will contain elements from index 2(including) till index 4(excluding)

```
var myarray = [length]datatype{values} // An array
myslice := myarray[start:end] // A slice made from the array
```

Lets see more examples

```
s := [6]int{10, 11, 12, 13, 14,15,16,17,19}
// first element
s[0]  // 10
s[0:1] //10
s[:1] //10

//last element
s[len(s)-1] //19
s[len(s)-1:len(s)] //19
s[len(s)-1:] //19

//first 5
s[:5] // 10 11 12 13 15

//last 5
s[len(s)-5:] // 14 15 16 17 19

//All
s[:] // 10 11 12 13 14 15 16 17 18 19
```

All other features mutating the value from array are also here in slices too.

**Append**

Append function can be used to append elements to a slices

```
s= append(s,5) //append new element 5 to slice s which returns the total updated slice s which we agin assing to s

s = append(s,4,5,6,7) // adds all the value in order to the slice s

s= append(s,b...) // appending all elemets of slice b to slice a
```

_Slices in go are like pointer that points to the underlying array it holds the address of the array._ This the reason **Slices are not comparable and we can compare slices to nil only and nil is the zero value of a slice.**


There is a inbuilt function called `Equal` from slices package to compare two slices value by value.


Nil and empty slice are different in go, lets demonstrate it.
```
var a []int
fmt.Println(a == nil) //true
a = []int{}
fmt.Println(a == nil)  //false
```

**As we know slice are just pointers to the underlying array so changes made on slices can affect the original array this affecting other slices refrrencing it.**

```
a:=[]int{1,2,3,4,5,6,7,8}
b:=a[2:]
b[0]=100
b = append(b,200)
fmt.Println(a)
fmt.Println(b)
```
Output
```
[1 2 100 4 5 6 7 8]
[100 4 5 6 7 8 200]
```

In the above code example we can see that we changed th first element of slice b to 100 which also altered the 2 index element of the slice a.

If we move the line `b = append(b,200)` above it will create new array for b and will not conflict with the array underlying a

```
a:=[]int{1,2,3,4,5,6,7,8}
b:=a[2:]
b = append(b,200)
b[0]=100
fmt.Println(a) //[1 2 3 4 5 6 7 8]
fmt.Println(b) // [100 4 5 6 7 8 200]
```

**Copy**

There is a inbuilt copy function in go which is generally used to copy all elements from one slice to another slice (only slice)

Thet copy function returns the no of elements copied and it will copy avaliable element even if the src or dest size are different.

```
package main

import "fmt"

func main() {
	src := []int{1, 2, 3}
	dest := make([]int, 3)

	n := copy(dest, src)

	fmt.Println("Copied:", n)        // Copied: 3
	fmt.Println("Destination:", dest) // Destination: [1 2 3]
}
```

**As we can slice an array to make it another slice, same we can slice a slice too.**
But we have to be very careful because a slice is pointing to a underlying array, when we slice the parent slice we get a child slice which is pointing to the same array as parent slice from its given index changes made on child slice can affect parent slice as well as the underlying array.

**After slicing the parent slice, the child slice gets capacity from the starting index up to the end of the underlying array — which is `cap(parent) - start index.`**

```
parent := []int{10, 20, 30, 40, 50}
child := parent[1:3]
fmt.Println("len(child):", len(child)) // 2
fmt.Println("cap(child):", cap(child)) // 4
```

### Strings Indepth

[Youtube: Strings](https://www.youtube.com/watch?v=hi-KJn6d428&list=PLq3etM-zISamTauFTO5-G5dqBN07ckzTk&index=23)

Strings are generally considered primitive data types in Go. However, in low-level languages like C which is close to Go in design, strings are not native types. Instead, we explicitly create a continuous array of characters to simulate a string. That’s why it's important to understand strings and their building blocks from a complex data type perspective, especially when working close to memory or performance.

- Strings are stored as sequence of Bytes and each byte can be accesed by its index notation and the slice expression also works with string
- In go strings are **immutable** once we create a string we can't change it
- Strings are made up of rune and bytes which can be inter converted from each other

```
s:="hello world"
string(s[0]) //"h"
string(s[:5]) //"hello"
string(s[:]) //"hello world"
s[1] = 'a' // error, strings are immutable
```
In the above example we see `s` variable is a string and we try to extract each element like slices. `s[0]` returns a byte which is 104 ascii for h we use `string` function to convert any ascii, unicode number to its mapped value and afte that we use slices notation to get part of word and at last we see that string on created can't be changed

- The byte data of string in assumed to be a UTF-8 encoded code point
- UTF-8 encoding and Unicode support means, any character of a string in Go can take 1 to 4 Bytes of memory
- if a code point takes more that 1 byte fetching byte data and using it directly can lead to unexpexted result for example s:="
हिन्दी", each character size can be more that 1 byte, accessing it `string(s[1])` can lead to unexpcted result, here comes Rune representing charactes for all unicode. rune is alisa for int32

Ways to get characters correctly

```
a := "हिन्दी"
	r := []rune(a)
  fmt.Println((r[0])) //2361
	fmt.Println(string(r[0])) //ह
```

We can convert a string to a slice of rune and access each index to get the unicode number of the character and wrapping it around string to get the point value of the unicode number

There are other inbuilt functions from utf-8, unicode library with lots of useful functions which can be used to work with rune values.

**Strings are immutable can't be changed but we can reassign the variable to another string**
```
name:="rehna"
name = "rajesh"
```
the block of character `rehan` will still be in memory it is not overwritter which will be managed by the garbage collector and the variable name will point to `rajesh` now

