# Functions

![functions](https://img.freepik.com/free-vector/scrum-method-concept-illustration_114360-13019.jpg?semt=ais_items_boosted&w=740)

A function is a reusable block of code designed to perform a specific task. Instead of writing the same code multiple times, you can define a function once and call it whenever needed. Functions improve code organization, readability, and maintainability by breaking down complex problems into smaller, manageable parts. Most programming languages, including Go, support functions as a core feature, enabling modular programming, logical separation of concerns, and easier debugging. Whether it’s performing a calculation, processing data, or handling user input, functions make your programs cleaner and more efficient.

```     
             Functions
           |            | 
Input ---> |    Code    | ---> Output
           |            | 
          
```



### Declaring and Calling Functions

[Resources](https://www.w3schools.com/go/go_functions.php)

```
func Sum(a,b int) int {
  return a+b
}
```

In the above code example we have declared a simple functions named Sum using th func keyword which returns sum of both input.

``` 
      Input arguments both of type int
         | |
func Sum(a,b int) int {
  return a+b        |______ Return type (int)
}                          

```
The two local variable a, b (for the function) are type of int which is expected while calling the function and that function return the sum of a and b which is also a int.

**All the variable declared inside a function are its local variable which can be only used inside the function and the variable passed in the function recives the copy of the acutal variable, changes made on them dont affect the original variable**

Although there are situations when we need to change the passed variable in that case we ise pointers, which we will discuss further.

It is not mandatory to have passed in arguments or return type in function

```
func hello(){
    fmt.Println("Hello")
}
```

Above function will just print "Hello" when the function is called.

**Calling a Function**

```
func hello(){
    fmt.Println("Hello")
}

func main(){
    hello() ----> name of the function followed by parenthesis
}
```

We can see in main function we call hello function using parenthesis, if there are arguments, it should be passed inside that parenthesis and use variable to capture the return value (if any).

```
func main(){
 a:=10
 b:=20
 var c int
 c = Sum(a,b)
 fmt.Println(c) // 30
}

func Sum(a,b int) int {
    return a + b
}
```

In the above function we can see how basic functions are declared and called.

**Returns**

In go we have to capibility of returning multiple values.
```
func divide(a, b int) (int, error) {
    if b == 0 {
        return 0, fmt.Errorf("cannot divide by zero")
    }
    return a / b, nil
}
```
Here in this function divide we take in 2 int and intend to return int and error (error is a data type we will be discussing further), if the Divisor is 0 it will return the value as 0 and custom error called 'cannot divide by zero'. If divisor is valid we will return the answer and `nil`(data type means nothing).

There is something called Named returns in go which is genarally not advised to use if the function is large, it is only best for small functions.

```
func rectangle(length, width int) (area int, perimeter int) {
    area = length * width
    perimeter = 2 * (length + width)
    return // returns area, perimeter
}
```

The above functions will return 2 int named area and perimeter which is declared in the function signature and inside the function we just use return keyword to return the variable mentioned in function signature.



### Variadic Parameters

[Youtube: Variadic](https://www.youtube.com/watch?v=iFiAQlbJoXY&list=PLq3etM-zISamTauFTO5-G5dqBN07ckzTk&index=36)

Variadic parameters are the variable number of argument passed into a functions, those type of functions are called variadic function. The most commonn variadic function in go is `fmt.Println` which can take in multiple argument.

```
func Sum(nums ...int) int {
  t:=0
  for _,num := range nums {
    t+=num
  }
  return t

}
```

In the above code we declared a function called Sum which takes in variable parameter of type int and the name for the variable is nums.

`...int` **This signifies a slice of int, slice is just an array with other functions in go we will be discussing it later.**

After taking in a slice of int we range over it (run through all int elements in the slice) and add that to the local variable `t` and return it.

**It is mandatory to have the variadic fucntion at the end of all arguments otherwise it will not compile.**

```
// This will not compile!
func invalid(nums ...int, msg string) {
    fmt.Println(msg, nums)
}

func valid(msg string, nums ...int) {
    fmt.Println(msg, nums)
}
```

### Understanding Functions

Functions in go are first class citizens, this means functions are treated like any other data we can assingn functions to variable, we can pass functions to another functions and even they can be returned in a function.



**Function signature** is simple code snippet which gives brief information about the function without the code in it, Some of the example are listed below
```
func sum(a,b int) int
func(int,int) int
func printName(name string)
func (string)
```


```
func main(){
  fullname := func(s1,s2 string) string {
    return fmt.Sprintf("%s %s", s1, s2)
  }

welcomestring := sayHello("code", "learned", fullname) 

fmt.Println(welcomestring)

}

func sayHello(fist,last string, fn func(string,string) string) string {
  fullname:= fn(first,last)
  return fmt.Sprintf("Welcome %s", fullname)
}

```

In the above function we initilized a function to fullname which takes in 2 string and return joining them. After that we call it `sayHello` function where we take in 2 string input mostly the name first and last and takes in a function whose signature is same as fullName function and the sayHello function returns a string inside it we create a `fullname` variable which contain the string returned by the function passed in sayHello, that is `fullName` (function in main block).

So we got `code learn` in fullname inside sayHello and then we return `welcome code learn`,
We capture that inside welcomeString in main block and print it

**Example**

```
package main

func multiplyBy(multiplier int) func (int) int {
  return func (i int) int {
    return i*multiplier
  }
}

func main() {
  multiplyby2 := multiplyBy(2)
  multiplyby3 := multiplyBy(3)

fmt.Println(multiplyby2(10)) // 20

}
```

In the above example, we have created a function called `multiplyBy` function which takes in multiplier and return the function which takes in a int and return the int multiplied by multiplier

We can create `multiplyby2`,`multiplyby3` etc functions and pass in respective value like 2,3 and those function can be used as function to double and triple

**Function Types**

The function signature works as its type, We use function signature to define what kind of function we want to recive or return. Genrally the functions signature are large so we cant use that large block of code again and again, we can make it a custom type which will enhances the code redibility

Lets update the multiplyBy code we saw previously

```
package main

type mignature func(int) int

func multiplyBy(multiplier int) mignature {
  return func (i int) int {
    return i*multiplier
  }
}

func main() {
  multiplyby2 := multiplyBy(2)
  multiplyby3 := multiplyBy(3)

fmt.Println(multiplyby2(10)) // 20

}
```

The above code didn't change much cause it is a simpler function but it will be used vastly to write clean and consise code which other can understand easily.

Here is another example:

```
type operation func (int,int) int

func main() {
  var peform operation
  peform = arithmeticOperation("add")
  result := peform(1,2)
  fmt.Println(result)
}

func arithmeticOperation(op string) operation {
  switch op {
    case "add":
        return func(n1,n2 int) int {
          return n1+n2
        }
    case "sub":
        return func(n1,n2 int) int {
          reutn n1-n2
        }

  }
}

```


### Anonymous Functions and Closures



