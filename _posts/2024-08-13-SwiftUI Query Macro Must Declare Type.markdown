---
layout: post
title: "SwiftUI Query Macro Must Declare Type"
date: 2024-08-13 10:17:00
category: programming
tags: [swift]
---

Error: Property missing a type annotation

```swift
@Query(sort: \Monster.name) private var monsters = [Monster]()  
```


Correct:  
```swift
@Query(sort: \Monster.name) private var monsters: [Monster] = []
```




[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

