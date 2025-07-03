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

[Resources]()

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





