---
layout: post
title: "Sort Bool In Swift"
date: 2024-06-07 22:48:00
category: programming
tags: [swift]
---

[SOLVED: How can I sort SwiftData Query results by a bool?](https://www.hackingwithswift.com/forums/swiftui/how-can-i-sort-swiftdata-query-results-by-a-bool/24680)


```swift
extension Bool: Comparable {
    public static fun <(lhs: Self, rhs: Self) -> Bool {
        // the only true inequality is false < true
        !lhs && rhs
    }
}
```




[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

