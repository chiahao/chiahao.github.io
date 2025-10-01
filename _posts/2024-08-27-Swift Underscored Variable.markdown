---
layout: post
title: "Swift Underscored Variable"
date: 2024-08-27 10:53:00
category: programming
tags: [swift]
---

### [Using conditionals inside template literals](https://stackoverflow.com/questions/65209314/what-does-the-underscore-mean-before-a-variable-in-swiftui-in-an-init)  

#### [Properties](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/properties/#Property-Wrappers)

```xml
self._momentDate is the Binding<Date> struct itself.
self.momentDate, equivalent to self._momentDate.wrappedValue, is a Date. You would use this when rendering the date in the view's body.
self.$momentDate, equivalent to self._momentDate.projectedValue, is also the Binding<Date>. You would pass this down to child views if they need to be able to change the date.
```

[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

