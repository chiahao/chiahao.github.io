---
layout: post
title: "SwiftUI Custom Initializer For Binding Property"
date: 2024-11-29 14:49:00
category: program
tags: [swiftdata]
---

```swift
struct FoodLogQuickAddView: View {
    @Binding var foodLog: FoodLog?
    @Query private var lastNightLogs: [FoodLog]
}
```

A custom initializer is required for lastNightLogs, which causes FoodLogQuickAddView   
to lose the compiler-generated memberwise initializer.

```swift
struct FoodLogQuickAddView: View {
    @Binding var foodLog: FoodLog?
    @Query private var lastNightLogs: [FoodLog]

    init(foodLog: Binding<FoodLog?>) {
        self._foodLog = foodLog
        
        _lastNightLogs = Query(filter: #Predicate<FoodLog> {
            ($0.occurredAt >= yesterdayStart) &&
            ($0.occurredAt < todayStart) &&
            ($0.dayPhase == nightRawValue)
        })
    }
}
```


[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

