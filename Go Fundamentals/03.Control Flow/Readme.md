# Control Flow

![image](https://cdn.dribbble.com/userupload/20489652/file/still-36425da9b4c7b2c9b7b54818c92b7608.gif?resize=400x0)

Control flow is one of the most fundamental aspects of any programming language. It defines the order in which individual statements, instructions, or function calls are executed. Without control flow, a program would simply execute line by line without any logic or decision-making ability.

In Go, control flow mechanisms are simple, clean, and powerful, allowing developers to build robust, readable, and maintainable code. Go favors clarity over cleverness, so its control structures avoid unnecessary complexity seen in other languages.

**Why is Control Flow Important?**

- It allows your program to make decisions (if, switch)

- Enables repetition and iteration (for, range)

- Handles exceptions and recovery (panic, recover)

- Helps implement branching logic and state management

Let's dive deep in the world of Control flow, exploring the use and working of control statements.

### If/Else

[Youtube: If/Else](https://www.youtube.com/watch?v=xAgtKW250ZU&list=PLq3etM-zISamTauFTO5-G5dqBN07ckzTk&index=29)

The `if` statement in Go allows us to execute a block of code if a given condition evaluates to true. Here’s the basic syntax:

```
package main

import "fmt"

func main() {
    age := 25 // declaring and initilizing age

    if age >= 18 { //false
        fmt.Println("You are an adult.") // dont print
    } 
}
```

Here in the above example we define if statement with `if` keyword and check weather the variable age is greter than equal to 18, if it is true it executes the block of code otherwise moves next.

**Else**

Else is just an extention of if statement, 
We can use the `else` statement to execute a different block of code when the condition in the `if` statement is false:

```
package main

import "fmt"

func main() {
    num := 15

    if num%2 == 0 { // if false executed else statement otherwise executes this block of code
        fmt.Println("The number is even.")
    } else {
        fmt.Println("The number is odd.")
    }
}
```

**if-else-if**

It is extention of If-else statement, it allows you to executes more than two condition, we can create a chain of if-else-if, if we are checking same variable or group of same variables.

```
package main

import "fmt"

func main() {
    num := 13

    if num == 10 { 
        fmt.Println("10")
    } else if num == 11 {
        fmt.Println("11")
    } else if num == 12 {
        fmt.Println("12")
    } else if num == 13 {
        fmt.Println("13")
    }
}
```

All if, if-else, if-else-if statment have a scope thing declared under the scope cna only be used inside it. 

There is a short variable declaration with if which declared as well as checks, and the variable can only be used insde the if and its chained if-else block.
```
if variable := expression; condition {
    // use variable
} else {
    // use variable here too
}
```

**Example:**
```
age:=19
if even := isEven(age); even {
    fmt.Println("Age is even")
}
```

Here in the above example isEven is a function that take in a number(int) and return true or false based on it nature, so in the even variable false is stored as 19 is not even after semicolon we check the condition which is false and will not exectes the block of code.



If statements can be nested too for multiple conditions check and it also follows scope policy the variable declared inside the nested if can be used inside that block, but the variable declared in the parent if can be used in nested if, its like global variable for the nested if.
```
num := 10
if num > 0 {
    a:=2 can be used in this scope and the nested scope inside it
    if num%2 == 0 {
        c:=a+2 // c can be used in this scope
        fmt.Println("Positive Even Number")
    }
}
```

### Switch 

[Youtube: Switch](https://www.youtube.com/watch?v=XkL6lEG8X7M&list=PLq3etM-zISamTauFTO5-G5dqBN07ckzTk&index=34)

The switch statement in Go is a multi-way branch that provides a clean alternative to long if-else-if chains. It allows you to match a value or condition against multiple cases, improving readability and efficiency.

**Basic Syntax**
```
switch expression {
case value1:
    // block for value1
case value2:
    // block for value2
default:
    // default block (optional)
}
```


**Example:**
```
day := "Monday"

switch day {
case "Monday":
    fmt.Println("Start of the week")
case "Friday":
    fmt.Println("Almost weekend")
default:
    fmt.Println("Some other day")
}

```

Here in the example above we have to initiate the switch block with `switch` keyword followed by the expression we need to check in this case it is a string, we start a code block inside that we check the value, it the value matches to the variable if executes the code otherwise it moves next until it finds default, then execute the code inside default and break out of switch. Unlike other programming languge like Java we dont need to use break in every case.

There can be multiple values in a case

```
day := "Sunday"

switch day {
case "Saturday", "Sunday": // if day is Sunday or Saturday it will excutes the code
    fmt.Println("Weekend")
default:
    fmt.Println("Weekday")
}

```

We can declare a variable and use switch on it, In a single line and the variable declared can only be used in that switch block of code, here is an example:
```
word:="Hello!"
switch wordLen:=len(word); wordLen {
    case wordLen < 7:
      fmt.Println("Short word")
    case wordLen > 6 &&  wordLen < 12:
      fmt.Println("Medium word")
    case wordLen > 12:
      fmt.Println("Long word")
    default:
      fmt.Println("word")
}
```

`len()` is a function which returns no of rune(characters) are there in the string.

**Fallthrough**

By default, cases do not fall through to the next one (unlike C/C++). But you can explicitly use fallthrough.

```
value := 2

switch value {
case 1:
    fmt.Println("One")
case 2:
    fmt.Println("Two")
    fallthrough
case 3:
    fmt.Println("Three")
    fallthrough
case 4:
    fmt.Println("Four")
default:
    fmt.Println("Default")
}
```
*Use fallthrough carefully – it does not check the next case condition, it blindly executes the next block.*

**Output:**
```
Two
Three
Four
Default
```
Line wise Explanation:

- Case 2 matched → prints "Two"
- fallthrough → does NOT check condition of case 3, just runs it

- Then fallthrough again → runs case 4

- Then goes to default


### Loops

[Resources: Blog](https://www.geeksforgeeks.org/go-language/loops-in-go-language/)

Go language contains only a single loop that is for-loop. A for loop is a repetition control structure that allows us to write a loop that is executed a specific number of times. In go there are multiple ways for loop can be used to peform different task

Thye basic syntax for `for loop` is very similar to other language.
```
for initialization; condition; post{
       // statements....
}
```

Here the initialization statement is **optional**, it executes before the loop starts, the condition holds a boolean expression which is checked at every iteration, if the value is true the loop executes. The post statement generally changes the value based on which the condition chnage to false to exit the loop.

```
// Go program to illustrate the  
// use of simple for loop 
package main

import "fmt"

// Main function
func main() {
    
    // for loop 
    // This loop starts when i = 0 
    // executes till i<4 condition is true
    // post statement is i++
    for i := 0; i < 4; i++{
      fmt.Printf("Hello World\n")  
    }
  
}
```
For loop can be used as infinite loop in go, it will executes **infinitely**.
```
for {
     // Statement...
}
```

**While loop** is not there in go unlike other programming language, but the concept of while is there which can be achived using for loop, here is an example
```
// Go program to illustrate the  
// the for loop as while Loop
package main

import "fmt"

// Main function
func main() {
    
    // while loop
    // for loop executes till 
    // i < 3 condition is true
    i:= 0
    for i < 3 {
       i += 2
    }
  fmt.Println(i) 
}
```

In the above program `for` keyword is followed by only `condition` just like while loop, and the statement executes until the condition is false.

**Ranges**

We can iterate through a loop until the condition is false, in this case we generally know about how many iterations we will have or the condition when will the loop stop.

Lets think about how we used to iterate through a Array elemnts, we get the length of array, start the loop from 0 to the length and get the element using `arr[i]`. There are different complex data types like array,slices,maps (group of data stacked), we have the feature called `range` to loop through all the elements contained in it 
```
// Go program to illustrate the  
// use of simple range loop 
package main

import "fmt"

// Main function
func main() {
    
    // Here rvariable is a array
    rvariable:= []string{"GFG", "Geeks", "GeeksforGeeks"} 
    
    // i and j stores the value of rvariable
    // i store index number of individual string and
    // j store individual string of the given array
    for i, j := range rvariable {
       fmt.Println(i, j) 
    }
  
}
```
**Output:**
```
0 GFG
1 Geeks
2 GeeksforGeeks
```

Here above we have an Array of three strings called rvariable, we loop through the rvariable with returns two variable i and j where i is index and j is the content for that index in this case it is string and index is always integer.

There are other complex types we can loop through like Slices and Maps, we will discuss it in their respective types.

We can loop through a **string** in go as well because string are just continous array like structure (We will discuss it further) which will return index and the char in the from of rune (character).

```
// Go program to illustrate the  
// use for loop using string
package main

import "fmt"

// Main function
func main() {
    
    // String as a range in the for loop
    for i, j:= range "XabCd" {
       fmt.Printf("The index number of %U is %d\n", j, i) 
    }
  
}
```

**Break and Continue**

Break and Continue are the most important control flow statements in loops.

**Break**

- Used to immediately exit the current loop (no further iterations).
- Commonly used when a condition is met early.

```
for i := 1; i <= 10; i++ {
	if i == 5 {
		break
	}
	fmt.Println(i)
}
```
**Continue** 

- Skips the rest of the current iteration and goes to the next loop cycle.

- Useful for ignoring specific values.

```
for i := 1; i <= 5; i++ {
	if i == 3 {
		continue
	}
	fmt.Println(i)
}
```

### Defer, Panic and Recover

[Resources: Blog](https://www.geeksforgeeks.org/go-language/go-defer-panic-and-recover/)

In Go, defer, panic, and recover are built-in mechanisms used for managing control flow and error handling. They are especially useful in handling unexpected runtime errors gracefully.

**Defer**

Defer, postpone execution until function ends,
Used to delay execution of a statement until the surrounding function returns.

```
package main

import "fmt"

func example() {
    defer fmt.Println("Deferred: 2")
    fmt.Println("Executing: 1")
}

func main() {
    example()
}
```

**Output:**
```
Executing: 1
Deferred: 2
```

It is mainly used to close files, unlocking mutexes and releasing resources (we will learn about all further)

In Go, each function call is stored in the call stack. When you use defer inside a function, the deferred function is not called immediately, but is scheduled to run after the surrounding function finishes, just before it returns.

If there are multiple deferred calls, they execute in Last-In-First-Out (LIFO) order. So, the last deferred call is executed first, and the first one last.

**Panic and Recover**

panic is a built-in function in Go that stops the execution of a program when an unrecoverable error occurs

**When panic is called?**

- The function where panic was called stops immediately.
- Any defer statements in that function run before it exits.
- Then the program goes back up the call stack, running deferred functions in each caller.
- If the panic is not recovered, the program crashes.

```
package main
import "fmt"

func division(num1, num2 int) {
    // if num2 is 0, program is terminated due to panic
    if num2 == 0 {
        panic("Cannot divide a number by zero")
    } else {
        result := num1 / num2
        fmt.Println("Result: ", result)
    }
}

func main() {
    division(4, 2)
    division(8, 0) // This will cause a panic
    division(2, 8) // This line will not execute
}
```
**Output:**
```
Result:  2
panic: Cannot divide a number by zero
```

Above is the example where we have a function which taked two int and return the queotient, but when it is divided by zero the program panics. It prints the result of first function call, the next function causes panic  and the next function call will not be exected.

**Recover**

While panic is used to terminate a program, recover is used to regain control after a panic has occurred. This allows the program to handle the error gracefully instead of crashing.

The recover function is used inside a deferred function to catch the panic message and resume normal execution. If recover is called outside of a deferred function, it has no effect.

```
package main
import "fmt"

// recover function to handle panic
func handlePanic() {
    // detect if panic occurs or not
    a := recover()

    if a != nil {
        fmt.Println("RECOVER:", a)
    }
}

func division(num1, num2 int) {
    // execute the handlePanic even after panic occurs
    defer handlePanic()

    // if num2 is 0, program is terminated due to panic
    if num2 == 0 {
        panic("Cannot divide a number by zero")
    } else {
        result := num1 / num2
        fmt.Println("Result:", result)
    }
}

func main() {
    division(4, 2)
    division(8, 0) // This will cause a panic, but it will be recovered
    division(2, 8)
}
```

**When to Use `defer`, `panic`, and `recover`**

- defer: Use defer for cleanup tasks, such as closing files, releasing locks, or logging. It ensures that resources are properly managed, even if an error occurs.
- panic: Use panic for unrecoverable errors, such as invalid input or system failures, where continuing execution would cause more harm.
- recover: Use recover to handle panics gracefully, especially in long-running applications like servers, where crashing is not an option.

