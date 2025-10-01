---
layout: post
title: "SwiftData Compare"
date: 2024-08-24 12:42:00
category: programming
tags: [swift]
---

Wrong:  

```swift
monsters.forEach { monster in
    if !collectedMonsters.contains(monster) {
        modelContext.insert(monster)
    }
}
```

Correct:  

```swift
monsters.forEach { monster in
    if !collectedMonsters.contains(where: { $0.no == monster.no }) {
        modelContext.insert(monster)
    }
}
```



[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

