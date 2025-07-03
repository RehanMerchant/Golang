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

**It is mandatory to have the variadic fucntion at the end of all arguments otherwise it will not compile**

```
// This will not compile!
func invalid(nums ...int, msg string) {
    fmt.Println(msg, nums)
}

func valid(msg string, nums ...int) {
    fmt.Println(msg, nums)
}
```