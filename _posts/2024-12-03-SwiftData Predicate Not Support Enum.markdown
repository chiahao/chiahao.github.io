---
layout: post
title: "SwiftData Predicate Not Support Enum"
date: 2024-12-03 14:49:00
category: program
tags: [swiftdata]
---

```shell
Query encountered an error: Unsupported Predicate: Captured/constant values of type 'DayPhase' are not supported
```

### Failure1
```swift
let night = DayPhase.night  

_lastNightLogs = Query(filter: #Predicate<FoodLog> {  
            ($0.occurredAt >= yesterdayStart) &&  
            ($0.occurredAt < todayStart) &&  
            ($0.dayPhase == night)  
        })
```

### Failure2
```swift
let nightRawValue = DayPhase.night.rawValue  

_lastNightLogs = Query(filter: #Predicate<FoodLog> {  
            ($0.occurredAt >= yesterdayStart) &&  
            ($0.occurredAt < todayStart) &&  
            ($0.dayPhase.rawValue == nightRawValue)  
        })
```


[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

