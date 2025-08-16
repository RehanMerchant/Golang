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