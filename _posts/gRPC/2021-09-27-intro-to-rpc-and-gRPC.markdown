---
layout: post
title:  "Introduction to RPC (and to an extent gRPC)"
date:   2021-09-27 21:42:47 +1000
categories: [rpc]
tags: [rpc, grpc, rest, api, protocol, protobuf, proto]
---

**Table of contents**
- [Introduction to RPC (and to an extent gRPC)](#introduction-to-rpc-and-to-an-extent-grpc)
- [What are Interservice communications?](#what-are-interservice-communications)
- [Interservice communication options](#interservice-communication-options)
  - [REST vs RPC](#rest-vs-rpc)
  - [gRPC](#grpc)


# Introduction to RPC (and to an extent gRPC)

I've always worked with REST APIs at work, in my personal projects etc. Whenever I wanted to build an API, I never even had to think twice about a different stratgey until now. I've read about RPCs at university, seen some examples and hear people talk about gRPC sometimes, but I never took took it seriously so far. So this is me trying to learn more about it, document my learnings so I can come back at a later stage and still remember what the heck gRPC is all about! 

If you have a subscription to Pluralsight, [this course](https://app.pluralsight.com/library/courses/grpc-enhancing-application-communication/table-of-contents) has great explanations for most of the gRPC stuff I've discussed below.


# What are Interservice communications?

In our current technology landscape, it is quite popular to split a product into smaller services and have them be independant of each other. In other words, we prefer `microservices architeture` where possible. The benefits of such architecture are many and not in scope of this post. But what is in scope is the way we *communicate* between these services to `get resources` or `perform some actions`.  

With microservice architecture comes the freedom to choose the best programming language for a particular service. Let's say as an example I have the following architecture:
- APIs hosted in EKS written in `C#`
- Identity service for Auth, written in `Go`
- A couple of lambdas behind an API gateway written in `python` and `JavaScript` 

<img src="/assets/images/grpc/grpc-microservice-architecture.jpg" alt="sample microservices with different languages" style="height: 400px; width: 800px" />


&nbsp; &nbsp; &nbsp;  
# Interservice communication options


For an architecture written in multiple languages such as above, there are two simple ways enable communication between them:
- Resource based communication via HTTP `(REST)` 
- Action based communication via `Remote Procedure Calls (RPC)`

&nbsp; &nbsp; &nbsp;  

![REST vs RPC (and gRPC)](/assets/images/grpc/grpc-comparison.jpg)

&nbsp; &nbsp; &nbsp;  
## REST vs RPC

---
I've tried to summarise some very basic differences between REST and RPC below

| S.No | REST (REpresenational State Transfer)               | RPC (Remote Procedure Call)                                                                   |
| ---- | --------------------------------------------------- | --------------------------------------------------------------------------------------------- |
| 1.   | Resource based communication                        | Action based communication                                                                    |
| 2.   | Loosely coupled between client, server and services | Tightly coupled - The caller must know both the method to call and all the response to expect |
| 3.   | Embraces HTTP semantics (`GET product/123`)         | Embraces programming semantics (function call such as `client.getProduct(ProductDetails)`)    |
| 4.   | Text based messaging                                | Binary based messaging, hence much more efficient and faster                                  |


&nbsp; &nbsp; &nbsp;  
## gRPC

---
gRPC, as you might have guessed, was developed by Google based on their internal tool called `Stubby` which they created to make interservice communication within Google products faster and efficient. Touching on some highlights about gRPC below:
- Cross-platform support
  - Supports a wide variety of languages (C++, Java, C#, Go, Python, Ruby to name a few)
- Supports *Streaming* content
  - aggregate multi-part requests and provide a single response or
  - send a stream of responses for a single request (video streaming, for example)
- Layered framework
  - The `gRPC` framerwork is isolated from the `transport protocol`
  - This enables to update gRPC framework andtTransport protocols independantly of each other
  - This also means that it is asy to replace the default transport protocol of gRPC from `protobuf` to something else like `json` 
- Exposes API via protobuf files 
- Generates gRPC code based on protobuf files as we build a project. These generated code enables a client to call gRPC method natively as if it was written in the same language