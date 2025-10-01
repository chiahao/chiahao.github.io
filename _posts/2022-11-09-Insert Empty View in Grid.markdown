---
layout: post
title: "Insert Empty View in Grid"
date: 2022-11-09 10:35:00
category: programming
tags: [swift, CS193P]
---

[SwiftUI Grid](https://sarunw.com/posts/swiftui-grid/)  

```swift
Grid {
	GridRow {
		ColorSquare(color: .pink)
		Color.clear
			.gridCellUnsizedAxes([.horizontal, .vertical])
		ColorSquare(color: .pink)
	}
	GridRow {
		ForEach(0..<3) { _ in
			ColorSquare(color: .green)
		}
	}
}
```

Results:  

|--|--|--|
|--|--|--|
|Pink||Pink|
|Green|Green|Green|


`gridCellUnsizedAxes`: Asks grid layouts not to offer the view extra size in the specified axes.




[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


