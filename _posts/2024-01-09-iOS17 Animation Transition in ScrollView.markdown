---
layout: post
title: "iOS17 Animation Transition in ScrollView"
date: 2024-01-09 09:16:00
category: swift
tags: [swift, iOS17, ScrollView]
---

```swift
ScrollView {
  VStack {
    ForEach(0 ..< 20) {
      i in
      Color.green
           .frame(width: 350, height: 200, alignment: .center)
           .cornerRadius(35)
           .scrollTransition(.interactive, axis: .vertical) { view, phase in
             view.opacity(phase.isIdentity? 0 : 1.0)
           }
    }
  }
}
```

### view transition phase:

topLeading / bottomTrailing -> identity phase (visible area) -> 

### ScrollTransitionPhase.isIdentity

```swift
view.opacity(phase.isIdentity? 0 : 1.0)
```

will show something in edging area but nothing in visible center area.  

```swift
view.opacity(phase.isIdentity? 1.0 : 0)
```

will show things become more solid from edging area.  


### ScrollTransitionPhase.value

> A phase-derived value that can be used to scale or otherwise modify effects.
> #### Discussion
> Returns -1.0 when in the topLeading phase, zero when in the identity phase, and 1.0 when in the bottomTrailing phase.

```swift
view.opacity(phase.value < 0 ? 0 : 1.0)
```


[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


