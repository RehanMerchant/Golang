# Pointers & Memory

![pointers](https://miro.medium.com/v2/resize:fit:1400/0*X8P2-BZ-evA5IZQg)


In Go, understanding how memory works is essential to writing efficient and effective programs. One powerful tool that gives you direct control over memory is the pointer. A pointer is a variable that stores the address of another variable, allowing you to access and modify values directly in memory. This can help avoid unnecessary copying of data, improve performance, and enable more flexible program behavior. While Go manages memory automatically with garbage collection, pointers still give you fine-grained control when you need it — especially when dealing with large data structures, structs, or passing values between functions.

Memory management is a crucial part of any programming language. It determines how your program allocates, uses, and frees memory while it runs. In Go, memory management is automatic, thanks to the garbage collector, but understanding how it works helps you write more efficient and bug-free programs.

So lets dive into understanding about pointers and further we will know about memory management which will be better understood after pointer.

#### Pointers

Resources: [Blog](https://www.geeksforgeeks.org/go-language/pointers-in-golang/) ,[Youtube](https://www.youtube.com/watch?v=eE9YrqQySOY&list=PLq3etM-zISamTauFTO5-G5dqBN07ckzTk&index=40)
 
Pointer in golang is a variable that store a memory address of another variable, it is a special variable. It stores the address in hexadecimal format. **Why is Pointers necessary?**, Each variables we declare or intilize in the program get stored in **RAM** in a specific address. To remember all the memory addresses(Hexadecimal Format) manually is an overhead that's why we use variables to store data and variables can be accessed just by using their name. While pointers are raw addresses of a variable, with which we can work efficiently with memory, share data between function etc.

- All pointers of any data type have the same size.
- The zero value for a pointer variable is nil

```
                   -----------------------------------
                   |  name        age        section |
                   |---------------------------------|
Variable Value --> |  rehan       19          "b02"  | 
       Address --> |  0x18        0x2         0x22   |
                   |                                 |
                   -----------------------------------
```

In the above illustration we can see variable value `rehan` for variable `name` stored in `0x18` address. Likewise variabel age and section are there. Using the memory address we can directly manipulate the stored value efficiently

**Pointer Operator**

When an asterisk is used as prefix with a variable type, it signifies that it store a pointer, (*) Operator is also called as derefrencing opreator, it can be also used to retrive the value stored at the address pointed to by a pointer. The (&) operator used as a prefix to a variable gets its memory address.

- Pointers cannot be created for constants or primitive literals.
- Attempting to derefrence a nil pointer will result in runtime panic.

Example
```
var pointertoInt *int
var pointertoString *string
var pointertoBool *bool

age:=10
pointertoInt = &age
ageValue:= *pointertoInt
```

In the above example,In the first three line we declare pointer variable which will point to int,string and bool types respectively. The astrisk as prefix before the datatype indicates that the variable are pointer types. After that we create an age variable which stores 10 as the value in memory, after that we use the pointer variable `pointertoInt` to store the address of the `age` variable, Now we can derefrence the pointer to get te value stored in that address.


- `var nameaddr *string`  num variable is a pointer that stores an address to a string data type value. Here we have only declared it, so it will have the zero value of pointer type (nil). On printing it will return nil.

- `name:="rehan"` We create a string datatype variable.

- `nameaddr = &name` here nameaddr store the address of the name variable.

- `name2:= *nameaddr` here the name2 will store the value inside the address we derefrence. 

 ```
 func main() {
a:= 10
increment(a)
fmt.Println(a) //10
 }

 func increment (x int){
  x++
 }
 ```
 In the above program it still prints 10, but we intended to print 11 but that don't happen because as we know in function the parameters we pass recive copy, but insted of passing variable, if we pass address of that we can achive what we want

 ```
  func main() {
a:= 10
increment(&a)
fmt.Println(a) //11
 }

 func increment (x *int){
  *x++
 }
 ```
 Now we pass the address of the variable `a` and derefrence it inside the increment function and increase the value, now it affects the same memory address that we print.

 #### Memory Management

 The process of allocationg, using and freeing memory during program execution efficiently such that the program functions fast and error free. (`malloc` and `free` are used in c/c++ to manage its own memory). But in go there is automatic memory management using garbage collector, reducing devloprt burden and preventing meomory leaks and dangling pointers, Unlike c/c++ where we have to manage all of it on our own.

 There are two memory in go **Stack** and **Heap**, Each have specific purpose

 **Stack**
 