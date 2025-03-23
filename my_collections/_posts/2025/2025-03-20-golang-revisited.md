---
layout: post
title: golang revisited
category: go
---

My book is showing its age, `go get` has been deprecated.

go is a typed language, compiled, but builds very fast.
Complexity is built up through use of interfaces and composition.
Functions can return multiple values ie `val, err := doSomeThing(oldVal)`
Doesn't need parenthesis on conditional statements like js does.
Doesn't need end of statement semicolon's the way js does.

goroutines for concurrency, channels to pass data
funcs starting with UpperCase are exported, lowerCase are not
package system
