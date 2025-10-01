---
layout: post
title: "SwiftData One-To-Many"
date: 2024-08-15 08:41:00
category: programming
tags: [swift]
---

### [How to create one-to-many relationships](https://www.hackingwithswift.com/quick-start/swiftdata/how-to-create-one-to-many-relationships)

> 1. If you intend to use inferred relationships, one side of your data must be optional.
> 2. If you use an explicit relationship where one side of your data is non-optional, be careful how you 
> delete objects - SwiftData uses the `.nullify` delete rule by default, which can put your data into 
> an invalid state.  To avoid this problem, either use an optional value, or use a `.cascade` delete rule.
> 3. Do not attempt to use collection types other than `Array`, because your code will simply not compile.

```swift
@Model class Movie {
	var name: String
	var releaseYear: Int  
	var director: Director?

	init( ...
}

@Model class Director {
	var name: String
	@Relationship(deleteRule: .nullify, inverse: \Movie.director) var movies: [Movie]
	
	init( ...
}
```

[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

