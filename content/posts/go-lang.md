+++
date = '2026-06-25T21:34:33+01:00'
draft = false
title = 'Go Lang'
+++

# Go in Comparison
Python is a great starting point for general programming and scripts. But when automation needs reliably across nodes, containers, or CI/CD pipelines, its additional layers slows it down. That is why infrastructure, Kubernetes, Docker, and Terraform are built in Go.

Bash shell scripting is a closely aligned to Go, in terms of its benefit and purpose. I believe Go is quicker to pickup and start using. However, more understanding is required to distinguish the differences.


# Go Wins
Go compiles into a single binary. 
Copy one file to a target, it runs -> no package managers, no runtime dependencies, and very small (>10MB)container images.

Go handles parallel execution with goroutines. Lightweight threads (~2 KB RAM) managed by the runtime. Thousands of concurrent network tasks without heavy memory usage.

Compiled Go binaries boot instantly with low memory requirement, great for system daemons, CLI tools, and automated CI/CD pipelines.


# **Go learning resources**

Learning Go by Jon Bodner - For engineers coming from Python or Java to learn how Gophers write clean code.

Go Web Examples (https://gowebexamples.com/): A lightweight guide focused on building web servers, routing, middleware, and handling JSON templates.  

The Go Programming Language by Donovan & Kernighan (Go lang creators) - "Go Bible" covers everything needed. i.e. types, packages, concurrency, low-level mechanics.

Go by Example (https://gobyexample.com/): Best for quick-reference. Short, executable code snippets side-by-side with  explanations.

# Go Exceptions
Working through Go, I would not want this to be the first language I learn. The very basics make sense such as the basic operators and keywords and procedural programming. 
Firstly, the acronyms create additional layers of complexity 

Secondly there are nil pointers, which are a strength, but will creates problems if implemented incorrectly.