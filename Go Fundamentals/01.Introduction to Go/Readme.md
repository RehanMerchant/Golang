# Introduction to Go

![Go_gif](https://miro.medium.com/v2/resize:fit:1400/0*NCKH5j7mncvMVBcR.gif)

Go, also known as golang is a open-source programming language devloped by **Google**. Designed for its simplicity, efficiency, and reliability.It has the ability to perform simple and fast like c and security benifits of c++ and ease of use of language.

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

Support for large scale programming was one of the main objectives. This had two aspects:

System scale: Greater support for concurrency was a must have and an efficient process level communication mechanism was desired along with speed of compilation.

Engineering scale: The objective was to develop a language for large codebases that are written and maintained by big teams.

**Safety**

Type safety: Nobody likes type issues to pop up at runtime in Production environment. So, being type-safe was important.

Memory safety: Nobody likes memory issues either. So, the ability to handle memory in a safe way mattered too.

**Better run-time**

A run-time environment with efficient, latency-free garbage collection was the target. In addition to that, they wanted to have built-in strings, maps and, communication channels for intra-thread communication.

**Better Package model**

A good package model goes a long way in keeping the code base maintainable. Explicit declaration of dependencies was a goal which would also help to improve build time.

### Why Go?

[Jetbrains Blog](https://blog.jetbrains.com/go/2021/02/03/the-state-of-go/) &
[Features Blog](https://benhoyt.com/writings/go-intro/)

As we discussed above the the goals of the language, which strongly suggest that the language is well designed.

Go is being used in many industries due to all of its feature.

![Go_Industry_Use](https://blog.jetbrains.com/wp-content/uploads/2021/02/4-2x.png)
_Image Source: Image found via [Jetbrains blog](https://blog.jetbrains.com/go/2021/02/03/the-state-of-go/). All rights belong to the original creator._

![Go_Industry_Use](https://blog.jetbrains.com/wp-content/uploads/2021/02/5-2x.png)
_Image Source: Image found via [Jetbrains blog](https://blog.jetbrains.com/go/2021/02/03/the-state-of-go/). All rights belong to the original creator._

They key features because of which go is so popular and used by top companies for their production applications and products are as follows:

- Small and simple core language. Go feels similar in size to C, with a very readable language spec that’s only about 50 pages long. This makes it easy to learn or teach to others.
- High quality standard library, especially for servers and network tasks.
- First class concurrency with goroutines (like threads, but lighter) and the go keyword to start a goroutine, channels for communicating between them, and a runtime whose scheduler coordinates all this.
- Compiles to native code, producing easy-to-deploy binaries on all the major platforms.
- Garbage collection that doesn’t require knob-tweaking
- Great documentation that is succinct and includes many runnable examples.
- Excellent tooling. Just type go build to build your project, go test to find and run your tests, etc. There’s CPU and memory profiling, code coverage, and cross compilation – all without external tooling.
- Heavily used in cloud tools. Docker and Kubernetes are written in Go, and Dropbox, Digital Ocean, Cloudflare, and many other companies use it extensively.

Go provide with a Wonderful standard library, that is extensive, cross-platform, and well documented. Go comes with “batteries included”, so you can build useful servers and CLI tools right away, without any third party dependencies.

### Installing and Setting up

You can head over to https://go.dev/doc/install, you can find proper download and install guide for your respective operating system.

**Environment Variable**

Before go version 1.11, go was supposed to setup in a particular manner very specific. Earlier there were no modules/package system in go. It was adviced to create a folder called **GOPATH**
(you can name it anything), but that folder contain three sub folder called `bin` `pkg` `src` Each folder has a particual purpose, the src folder contans all raw go source code organized by import path, it also contain all the downladed packages also.
The pkg folder stores `.a` files (Go package archives), generallly used to speed up the compilation and the bin folder store the binary executable of the raw files from the src folder.

As of **Go 1.11+**, Go used Module system which dont require GOPATH. Your project structure can be anywhere on your machine.
We will discuss it in more depth further.
