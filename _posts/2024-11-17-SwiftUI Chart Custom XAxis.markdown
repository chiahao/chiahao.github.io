---
layout: post
title: "SwiftUI Chart Custom XAxis"
date: 2024-11-17 12:29:00
category: swift
tags: [swiftui, chart]
---

```swift
.chartXAxis{
AxisMarks(values: xAxisValues()) { value in
    AxisValueLabel(
        format: .dateTime.day().month(),
        centered: true
    )
}
```

[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

