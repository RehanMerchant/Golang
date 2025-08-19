# Error

![image](https://miro.medium.com/1*ZvwdIQkolJ2z1MILFrQjOQ.jpeg)


 Go has a very different way of handling errors, There is no try-catch but it uses if checks for error handling. The **last return value** is error by convetion and the error string follows a non captalized and non puntuations ending convection.
 
 **The Error Interface**

 The error type is an interface type in go, it has a single method called error returning a string.

```
type error interface {
    Error() string
}
```

#### Hadling Errors

There are three methods widely used to create errors

- Implement the error interface

```
type MyError struct {
    Code int
    Msg  string
}

func (e *MyError) Error() string {
    return fmt.Sprintf("Code %d: %s", e.Code, e.Msg)
}

func doSomething() error {
    return &MyError{Code: 404, Msg: "Resource not found"}
}

func main() {
    err := doSomething()
    if err != nil {
        fmt.Println(err) // Code 404: Resource not found
    }
}
```

in the above example we create a type called `MyError` which holds code and Msg and we create a method linked to that struct called Error whoch prints the errorcode and message, In main function we call doSomething function which simply returns the error and if we catch some error (not nil) it prints the error


- Using errors.New

```
func Divide(a,b float64) (float64,error) {
    if b==0{
        return 0, errors.New("cannot divide by zero")
    }
    return a/b, nil
}

func main(){
    result,err:=Divide(10,2)
    if err != nil {
        fmt.Println("error ",err)
        return
    }
    fmt.Println("result: ", result)
}

```

In the above program we use predefined functions from errors package called `New` which create a default error type and after that in main function we use if checks to identify errors and handle it.

- Using fmt.Errorf

```
func Divide(a,b float64) (float64,error) {
    if b==0{
        return 0, fmt.Errorf("cannot divide by zero")
    }            
    return a/b, nil
}
```

It is same as before but we use a Errorf function from fmt package instead of New function from errors package.


#### Sentinel and Wrapping Error

Sentenial errors indicate3 occurance of a unique event. it is exported as package level variables, they need to be maintaned along with other parts of the code.

example from `database/sql` package where

```
var ErrNoRows = errors.New("sql:no rows in result set")
```
we check this specific error and handel error specifically `if err == sql.ErrNoRows`

example

```
import "errors"

var ErrNotFound = errors.New("not found")

func findUser(id int) (string, error) {
    if id == 0 {
        return "", ErrNotFound
    }
    return "Alice", nil
}

func main() {
    user, err := findUser(0)
    if err != nil {
        if err == ErrNotFound {
            fmt.Println("User not found")
        } else {
            fmt.Println("Other error:", err)
        }
    } else {
        fmt.Println("Found:", user)
    }
}
```

in the above program we create a custom error called ErrNotFound which we can use to check and handel the error specifically.

The problem with sentinel errors is that if we wrap an error with extra content, the direct comparasion fails and it leads to tight coupling between packages.


**Error Wrapping**

When you return an error from one function, you often want to add context about what failed.
Example: Instead of just "not found", return "loading user profile: not found".

example

```
func readFile() error {
    return io.EOF // end of file error
}

func process() error {
    if err := readFile(); err != nil {
        return fmt.Errorf("process failed: %w", err)
    }
    return nil
}

func main() {
    err := process()
    if errors.Is(err, io.EOF) {
        fmt.Println("Detected EOF error inside wrapped error")
    }
}

```

in the above program, we create a readFile function which simply returns an error from io package called EOF (End of file), after that we create process function (a wrapper funtion) which checks the error by callig the first function if it is not nil it returns a modified error. In the main function we call the second function that is process and we use `Is` function from errors package to compare the error we got from second function with the io.Eof error it is true if prints the following statements.

- readFile returns a low-level error (io.EOF).
- process wraps it with extra context.
- main can still check the original cause using errorsIs

We can use errors.Join to print multiple levels of error like before

```
func secondFunction() error {
    firstErr := firstFunction()
    if firstErr != nil {
        secondErr:=errors.New("failed in second error)
        return error.Join(firstErr,secondErr)
    }
}
```

**In the above code we wrap an error inside another error with some more content for programmer, we can unwrap error too in go using Unwrap method**


```
func readFile() error {
    return io.EOF // end of file error
}

func process() error {
    if err := readFile(); err != nil {
        return fmt.Errorf("process failed: %w", err)
    }
    return nil
}

func main() {
    err := process()
    if errors.Is(err, io.EOF) {
        fmt.Println("Detected EOF error inside wrapped error")
    }

    innerError := errors.Unwrap(err)
    fmt.Println("Inner error: ",innerError)
}

```

#### Comparing Errors

There are mainly three ways we can compare errors in go

- Direct Equality (==)

Errors in Go are just values. You can compare them with == if they are the exact same value.

```
var ErrNotFound = errors.New("not found")

func findItem(id int) error {
    if id == 0 {
        return ErrNotFound
    }
    return nil
}

func main() {
    err := findItem(0)
    if err == ErrNotFound {
        fmt.Println("Item not found")
    }
}

```

only works for sentinel errors, fails when we wrap the error.

- errors.Is

Checks if an error is a target error, even if wrapped.

```
import (
    "errors"
    "fmt"
)

var ErrNotFound = errors.New("not found")

func getUser() error {
    return fmt.Errorf("db query failed: %w", ErrNotFound)
}

func main() {
    err := getUser()
    if errors.Is(err, ErrNotFound) {
        fmt.Println("Handled: user not found")
    }
}

```

Use errors.Is for sentinel errors with wrapping support.

- errors.As

Checks if an error is of a specific type (or wraps one), and if so, assigns it to a variable.
errors.As is used when you want to check if an error is of a certain type (not just value).
It also extracts that error into a variable so you can use its fields.

```
package main

import (
    "errors"
    "fmt"
    "os"
)

func readFile() error {
    _, err := os.Open("missing.txt")
    return err
}

func main() {
    err := readFile()

    var pathErr *os.PathError
    if errors.As(err, &pathErr) {
        fmt.Println("A PathError happened!")
        fmt.Println("Operation:", pathErr.Op)
        fmt.Println("File Path:", pathErr.Path)
        fmt.Println("Underlying error:", pathErr.Err)
    } else {
        fmt.Println("Some other error:", err)
    }
}

```

Output

```
A PathError happened!
Operation: open
File Path: missing.txt
Underlying error: no such file or directory
```

- os.Open returns an *os.PathError (a struct with fields).
- errors.As(err, &pathErr) → checks if err (or what it wraps) is of type *os.PathError.
- If yes, Go assigns the actual error to pathErr.
- Now you can inspect fields like .Op, .Path, .Err.