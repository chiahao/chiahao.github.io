---
layout: post
title: "SwiftUI Result of NavigationLink initializer is unused"
date: 2024-08-19 09:28:00
category: programming
tags: [swift]
---

### View1

```swift
Text("\(account.crystal.sorted(by: {$0.timestamp > $1.timestamp}).first?.amount ?? 0)")
```

### View2

```swift
let newCrystalRecord = Crystal(timestamp: timestamp, amount: stoneAmount)
newCrystalRecord.account = account
modelContext.insert(newCrystalRecord)
```

When add crystal in View2, the Text in View1 won't update immediagely.  


### Rewrite View2:  

```swift
let newCrystalRecord = Crystal(timestamp: timestamp, amount: stoneAmount)
newCrystalRecord.account = account
account.crystals.append(newCrystalRecord)
modelContext.insert(newCrystalRecord)
```

[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

