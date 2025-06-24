# Introduction to Go

Go, also known as golang is a   open-source programming language devloped by **Google**. Designed for its  simplicity, efficiency, and reliability.It has the ability to perform simple and fast like c and security benifits of c++ and ease of use of language.

### The Origin Story
[Read the Original Post](https://medium.com/geekculture/learn-go-part-1-the-beginning-723746f2e8b0)


The story of **Go** began mid 2007 at Google. Robert Griesemer, Rob Pike and Ken Thompson faced challenges tackling some problems at Google, due to it's scale of operations, The selection criteria for the Programming Language was tight. Their main considerations was a **efficient compilation, efficient execution and ease of programming language.** 

Though they evaluated many of the existing languages, they couldn’t find any language which offered all three of their primary considerations.That realization led them to think about creating a new programming language. Thus, the seeds to develop Go were planted.

The design began in September 2007 as a 20% project at Google. As things progressed, many others joined as well. In January 2008, work on initial compiler started. The language was open-sourced later in November 2009. It took a few more years to release first stable version Go, in March 2012. Thus, the story of Go started and continues ever since.

### Design Goals

[Read the Original Post](https://medium.com/geekculture/learn-go-part-1-the-beginning-723746f2e8b0)

The devlopers of go have few things in their mind while making go, that shaped the future of go

**Simplicity**

First and foremost, a simple language with clean, concise syntax was the target. A lightweight type system, with no type hierarchy.


**Scale**

Support for large scale programming was one of the main objectives.

**Safety**

Type safety and Memory safety was the foremost important features that is there in go which prevents production faliure and memory issues.

**Better run-time**

A run-time environment with efficient, latency-free garbage collection was the target.

**Better Package model**

A good package model goes a long way in keeping the code base maintainable. Explicit declaration of dependencies was a goal which would also help to improve build time.


### Why Go?

As we discussed above the the goals of the language, which strongly suggest that the language is well designed. 

Go is being used in many industries due to all of its feature.

![Go_Industry_Use](https://blog.jetbrains.com/wp-content/uploads/2021/02/4-2x.png)
*Image Source: Image found via [Jetbrains blog](https://blog.jetbrains.com/go/2021/02/03/the-state-of-go/). All rights belong to the original creator.*

![Go_Industry_Use](https://blog.jetbrains.com/wp-content/uploads/2021/02/5-2x.png)
*Image Source: Image found via [Jetbrains blog](https://blog.jetbrains.com/go/2021/02/03/the-state-of-go/). All rights belong to the original creator.*

They key features because of which go is so popular are as follows

- Small and simple core language. Go feels similar in size to C, with a very readable language spec that’s only about 50 pages long. This makes it easy to learn or teach to others.
- High quality standard library, especially for servers and network tasks.
- First class concurrency with goroutines (like threads, but lighter) and the go keyword to start a goroutine, channels for communicating between them, and a runtime whose scheduler coordinates all this.
- Compiles to native code, producing easy-to-deploy binaries on all the major platforms.
- Garbage collection that doesn’t require knob-tweaking
- Great documentation that is succinct and includes many runnable examples.
- Excellent tooling. Just type go build to build your project, go test to find and run your tests, etc. There’s CPU and memory profiling, code coverage, and cross compilation – all without external tooling.
- Heavily used in cloud tools. Docker and Kubernetes are written in Go, and Dropbox, Digital Ocean, Cloudflare, and many other companies use it extensively.

Go provide with a Wonderful standard library, that is extensive, cross-platform, and well documented. Go comes with “batteries included”, so you can build useful servers and CLI tools right away, without any third party dependencies.


