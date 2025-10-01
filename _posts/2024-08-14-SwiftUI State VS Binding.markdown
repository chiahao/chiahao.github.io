---
layout: post
title: "SwiftUI State VS Binding"
date: 2024-08-14 10:36:00
category: programming
tags: [swift]
---

### [@State @Binding in SwiftUI with example and explanation](https://medium.com/@ramdhas/state-binding-in-swiftui-60ee2feed2b1)

> @Binding: Used to create a two-way connection between a parent view and its child view. 
> It allows the child view to read and modify a value owned by the parent view.

```swift
struct ParentView: View {
	@State private var toggleState = false

	var body: some View {
		VStack {
			ChildView(isToggled: $toggleState)
			Text("Toggle State: \(toggleState.description)")
		}
	}
}

struct ChildView: View {
	@Binding var isToggled: Bool

	var body: some body {
		Toggle("Toggle", isOn: $isToggled)
	}
}
```

[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

