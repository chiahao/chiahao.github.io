---
layout: post
title: "CS193P Lecture07-ViewModifier Animation"
date: 2022-11-07 10:35:00
category: programming
tags: [swift, CS193P]
---

1. by animation a Shape
2. animation via their ViewModifiers

```swift
protocol ViewModifier {
   typealias Content // the type of the View passed to body(content:)
   func body(content: Content) -> some View {
      return some View that almost certainly contains the View 
   }
}
```

### Important takeaways about Animation

#### Only <u>changes</u> can be animated.  Changes to what?
1. ViewModifier arguments  
2. Shapes  
3. The "existence" (or not) of a View in the UI  
(the comings and goings of Views)

#### Anmation is showing the user <u>changes that have already happened </u>(i.e. the recent past).



[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


