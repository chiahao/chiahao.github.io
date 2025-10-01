---
layout: post
title: "9-SwiftData Dynamically Query Filter"
date: 2024-11-29 14:49:00
category: program
tags: [swiftdata]
---

According to [Dynamically filtering our SwiftData query](https://www.hackingwithswift.com/books/ios-swiftui/dynamically-filtering-our-swiftdata-query),  

Predicate still needs the value to be directly inlined as a constant!  


These two not work!  
```swift
enum DayPhase {
    case morning
    case night

    static var morningRawValue: String {
        DayPhase.morning.rawValue
    }

    static let morningRawValue = "morning"
}
```

```swift
@Query(filter: #Predicate<FoodLog> { ($0.occurredAt >= yesterdayStart) && ($0.occurredAt < todayStart) && ($0.dayPhase.rawValue == DayPhase.nightRawValue) }) private var yesterdayNightAfterLog2: [FoodLog]
```

But it works inside `init`:  

```swift
@Query private var yesterdayNightAfterLog: [FoodLog]

init() {  
    let yesterdayStart = Calendar.current.startOfDay(for: Calendar.current.date(byAdding: .day, value: -1, to: .now)!)  
    let todayStart = Calendar.current.startOfDay(for: .now)  
    let nightRawValue = DayPhase.night.rawValue  
    
    _yesterdayNightAfterLog = Query(filter: #Predicate<FoodLog> { ($0.occurredAt >= yesterdayStart) && ($0.occurredAt < todayStart) && ($0.dayPhase.rawValue == nightRawValue) })  
}
```


[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

