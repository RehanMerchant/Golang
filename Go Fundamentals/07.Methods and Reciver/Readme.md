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

