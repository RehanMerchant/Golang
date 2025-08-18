# Interfaces

![image](https://media.istockphoto.com/id/1358014160/photo/we-need-to-focus-on-our-future-goals.jpg?s=612x612&w=0&k=20&c=5CgI_OQ-ieQjEBXMkyhFjHGgnVndbc1ClEIWpIOxP8c=)

Interfaces are abstract types that specify functionality. To implement the interface, a type must satify all the methods in the interface.

#### Interface

an interface defines a set of methods that **an type must have in order to satisfy it**.

In go interfaces are implicitly implemented unlike Java where we have to use `implements` keywoard to implement.

Lets declare function in a interface
```
type Shape interface{
    Area() float64
}

type Car interface {
    Start()
    Stop() bool
}
```

Here above in the code we define two interface `Shape` which declare Area function and `Car` which declare Start and Stop fucntions

The type using the Area function automatically implements the Shape interface and the type using the Start and Stop methods implements Car interface.

```
type Shape interface {
    Area() float64
}

type Rectangel structs {
    Width float64
    Height float64
}

func(r Rectangel) Area() float64 {
 return r.Width * r.Height
}

type Circle structs {
    Radius float64
}

func(c Circle) Area() float64 {
 return 3.14*c.Radius*c.Radius
}

func main(){
    rectangel:= Rectangel{Width:5,Height:3}
    circle:=Circle{Radius:5}

    shapes:= []Shape{rectangel,circle}

    for _,shape:= range shapes {
        fmt.Printf("Area:%f\n", shape.Area())
    }
}

```
In the above example we create a interface called Shape which has a function signature called Area(), after that we declare two structs type called Rectangle and Circle which uses the Area function as reciver methods, that means the two structs types implemented the interface Shape. In main function we decalare two Rectangle and Circle types variable with their respective value and then created a slice of Shape(interface) that holds the the two declared variable(as they satisfy the Shape interface). After that we loop through shape slice printing the area of each shape. **If a type does not satisfy or implement the shape interface can be used inside the shape slice**

There can be **nested interface** too, to satisty that interface we have to completely implement the methods declared exclusively in that interface as well as all the methods of the nested interface.


**Empty Interface**

Empty interface have no type of value. The pre-declared indetifier `any` is a alias of  `interface{}`,It is used when you want to store any kind of value specially when the type of value is not known, as go is strongly typed laungage it is necessary to spicify types. example is parsing a `json document` where we dont have nay idea what type each fields can be. **Every type in go implements it**.

```
func describe(i interface{}) {
    fmt.Printf("Value: %v, Type: %T\n", i, i)
}

func main() {
    describe(42)
    describe("hello")
    describe(true)
}
```

#### Type Assertions & Switch

There are times when you need to derive back the type from an empty interface. There are multiple methods of doing it, like using the reflection package, type assertion and type switch etc.

**Type assertion**

Type assertion is used to assert type for an empty interface.

```
func main(){
    var emptyinterface any
    emptyinterface = "Hello World!"

    if str,ok:=emptyinterface.(string); ok {
         fmt.Println("the value:", str)
    }
}
```

the above program will print the value:Hello World!, as it is a type of string. It is adviced to use the if check to provide a extra level of validation.

**Tyee switch**

Type switch can be used to check against multiple types and it is done in switch statement instead of switching values. Inside each case the value will of that type if the case matches, otherwise it remains empty.

```
func checkType(value interface{}) {
    switch v:=value.(type){
        case int:
        fmt.Println("Int")
        case string:
        fmt.Println("String")
        case float64:
        fmt.Println("Decimal")
        default:
        fmt.Println("Unknown type")
    }
}

func main() {
    checkType(44) //int
    checkType("Hello") //string
    checkType(3.43) //decimal
    checkType(true) //unknown type
}
```

in the above program we create a `checkType` function which check `any` value and determine its type, if not found prints default statement. In main function we call the function and the output is beside it