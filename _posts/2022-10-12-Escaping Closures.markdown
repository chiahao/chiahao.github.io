---
layout: post
title: "Escaping Closures"
date: 2022-10-12 13:39:00
category: programming
tags: [swift]
---



### Escaping Closures
> A closure is said to escape a function when the closure is passed as an argument to the function, but is called after the function returns.
>
> As an example, many functions that start an asynchronous operation take a closure argument as a completion handler.

```swift
var completionHandlers: [() -> Void] = []
func someFunctionWithEscapingClosure(completionHandler: @escaping () -> Void) {
	completionHandlers.append(completionHandler)
}
```

### Avoid Strong Reference Cycle

> If you want to capture `self`, write `self` explicityly when you use it, or include `self` in the closure's capture list.  Writing `self` explicitly let you express your intent, and reminds you to confirm that there isn't a reference cycle.


```swift
func someFunctionWithNonescapingClosure(closure: () -> Void) {
	closure()
}

class SomeClass {
	var x = 10
	func doSomething() {
		someFunctionWithEscapingClosure { self.x = 100 }
		someFunctionWithNonescapingClosure { x = 200 }
	}
}

let instance = SomeClass()
instance.doSomething()
print(instance.x)
// Prints "200"

completionHandlers.first?()
print(instance.x)
// Prints "100"
```


### Escaping closure can't capture a mutable reference to `self` when `self` is an instance of a structure or an enumeration.
Structures and enumerations don't allow shared mutability.

```swift
struct SomeStruct {
	var x = 10
	mutating func doSomething() {
		someFunctionWithNonescapingClosure { x = 200 }	// Ok
		someFunctionWithEscapingClosure { x = 100 }		// Error
	}
}
```


[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


