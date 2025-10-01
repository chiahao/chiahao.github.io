---
layout: post
title: "Displaying Dynamic Dates in Widgets"
date: 2022-10-12 10:14:00
category: programming
tags: [swift]
---


[Displaying Dynamic Dates in Widgets](https://developer.apple.com/documentation/widgetkit/displaying-dynamic-dates)


```swift
let components = DateComponents(minute; 11, second: 14)
let futureDate = Calendar.current.date(byAdding: components, to: Date())!

Text(futureDate, style: .relative)
// Displays:
// 11 min, 14 sec

Text(futureDate, style: .offset)
// Displays:
// -11 minutes
```

1. relative: absolute difference between the current date and time and the date specified
2. offset: the difference between the current date and time and the date specified. future with (-); past with (+).


```swift
let components = DateComponents(minute: 15)
let futureDate = Calendar.current.date(byAdding: components, to: Date())!

Text(futureDate, style: .timer)
// Displays:
// 15:00
```
3. timeer: counts up when the date passes.

```swift
// Absolute Date or Time
let components = DateComponents(year: 2020, month: 4, day: 1, hour: 9, minute: 41)
let aprilFirstDate = Calendar.current(components)!

Text(aprilFirstDate, style: .date)
Text("Date: \(aprilFirstDate, style: .date)")
Text("Time: \(aprilFirstDate, style: .time)")

// Displays:
// April 1, 2020
// Date: April 1, 2020
// Time: 9:41AM
```

```swift
// time interval
let startComponents = DateComponents(hour: 9, minute: 30)
let startDate = Calendar.current.date(from: startComponents)!

let endComponents = DateComponents(hour: 14, minute: 45)
let endDate = Calendar.current.date(from: endComponents)!

Text(startDate ... endDate)
Text("The meeting will take place: \(startDate ... endDate)")
```

[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


