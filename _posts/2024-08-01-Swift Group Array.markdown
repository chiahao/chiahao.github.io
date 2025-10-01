---
layout: post
title: "Swift Group Array"
date: 2024-08-01 08:06:00
category: programming
tags: [swift]
---

```swift
let stopsGrouped: [[Stop]] = [_](Dictionary.init(grouping: stops, by: \.routeId).values)
```

`[_]` is equivalent to `Array()`:  

```swift
let stopsGrouped: [[Stop]] = Array(Dictionary.init(grouping: stops, by: \.routeId).values)
```


[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

