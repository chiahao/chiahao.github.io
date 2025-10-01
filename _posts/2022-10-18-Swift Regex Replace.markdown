---
layout: post
title: "Swift Regex Replace"
date: 2022-10-18 11:23:00
category: programming
tags: [swift, regex]
---

```swift
var str = "123ABC456 789abc012"
_ = str.replacingOccurrences(of: "[a-zA-Z]", with: "-", options: .regularExpress, range: nil)

// output
// 123---456 789---012
```


[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


