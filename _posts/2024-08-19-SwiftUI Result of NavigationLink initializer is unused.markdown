---
layout: post
title: "SwiftUI Result of NavigationLink initializer is unused"
date: 2024-08-19 09:28:00
category: programming
tags: [swift]
---

### [Result of 'NavigationLink<Label, Destination>' initializer is unused](https://stackoverflow.com/questions/75678396/result-of-navigationlinklabel-destination-initializer-is-unused)

Instead of this:

```swift
.toolbar {
	ToolbarItemGroup(placement: .primaryAction) {
	    Button("Edit Collected Monster", systemImage: "gear") {
	    	NavigationLink("", destination: MonsterSearchView())
	    }
```

Use this:

```swift
.toolbar {
	ToolbarItemGroup(placement: .primaryAction) {
		NavigationLink(destination: MonsterSearchView(), label: {
			Image(systemName: "gear")
		})
```


[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

