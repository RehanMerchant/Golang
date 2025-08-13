# Methods and Reciver

![image](https://www.21kschool.com/in/wp-content/uploads/sites/4/2024/09/Learning-Methods.png)


In Go, methods are functions with a special receiver argument. They allow you to define behavior (functions) that is associated with a type—this brings Go closer to object-oriented programming without actual classes.

#### Methods

Methods are functions that are associated and belong to a type.
We can defile methods for both custom or derived types.

``` 
type Person struct {
    Name string
    Age int
}

func(p Person) getDetails() string {
return fmt.Printf("Name: %s, Age: %d",p.Name,p.Age)
}
```
Here in the above code function *getDetails* is associated to Person type which makes it a method.

**There is no concept like method overloading in Go.**

#### Receiver Types

```
type Rect struct{
    Length float64
    Width float64
}

func(r Rect) Area() float64{
    return r.Length * r.Width
}

func main(){

rectangle:=Rect{Length:5.0, Width:2.0}

fmt.Println(rectangle.Area())

}

```

In the above program Rect type have a function Area linked to it which returns the area of the Rect type associated to it. In the main function we decalre a type rectangle with a definite length and width and we used the Area method to print the are that is 10.0

**Like functions methods also recive copy of the associated type so we have to use the pointer of that type**

```
func(r *Rect) Area() float64{
    return r.Length * r.Width
}
```
The abover reciver type is called **Pointer Reciver** where we recive pointers and before that the example is called **Value Reciver**.


**Nil Pointer**

```
func main(){

var rectangle *Rect

fmt.Println(rectangle.Area())

}

```

Here above on calling method associated to a nil pointer causes a runtime error.

What we can do: add a check in the merthod to return something if the pointer is nil

```
func(r *Rect) Area() float64{
    if r== nil{
        return 0
    }
    return r.Length * r.Width
}
```

**Methods Set Rules**

In Go, the method set determines which methods a type has

For a value T: Method set includes all methods with value receivers.

For a pointer *T:Method set includes both value and pointer receiver methods.

```
type T struct{}

func (t T) Val()   {}
func (t *T) Ptr()  {}

func main() {
    var v T
    v.Val()  
 // v.Ptr() // ERROR: T has no method Ptr

    var p *T
    p.Val()  
    p.Ptr()  
}
```
In the above code we have two methods associated with struct type T `Val` and `Ptr`. In main function we declare `v` variable with type T, we can call Val on that but not Ptr because it asks for a pointer.

But both Val and Ptr will work if the variable type is a pointer. If the reciver is a pointer, go will automatically derefrence to call value-reciver method.

