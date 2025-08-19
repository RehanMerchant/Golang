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

