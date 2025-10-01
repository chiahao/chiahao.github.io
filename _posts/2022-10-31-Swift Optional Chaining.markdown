---
layout: post
title: "Swift Optional Chaining"
date: 2022-10-31 11:25:00
category: programming
tags: [swift]
---

### Optional Chaining

```swift
class Address {
	var buildingName: String?
}

class Person {
	var address: Address?
}

func createBuildingName() -> String {
	print("createBuildingName was called.")
	return "12"
}

let john = Person()
john.address?.buildingName = createBuildingName()
```

nothing was printed, because function was not called.


[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


