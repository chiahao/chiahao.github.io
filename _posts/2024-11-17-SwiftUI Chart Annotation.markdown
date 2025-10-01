---
layout: post
title: "SwiftUI Chart Annotation"
date: 2024-11-17 12:29:00
category: swift
tags: [swiftui, chart]
---

```swift
import SwiftUI
import Charts
import Foundation

struct SimpleAnnotationView: View {
    
    private var intakes: [Intake] = [
        Intake(timestamp: .now, dayPeriod: true, amount: 55),
        Intake(timestamp: Calendar.current.date(bySetting: .day, value: 1, of: .now)!, dayPeriod: true, amount: 55),
    ]
    @State private var rawSelectedDate: Date?
    var selectedDate: Date? {
        guard let rawSelectedDate else { return nil }
        return intakes.first(where: {
            Calendar.current.startOfDay(for:$0.timestamp) == Calendar.current.startOfDay(for: rawSelectedDate)
        })?.timestamp
    }
    
    var body: some View {
        Chart {
            ForEach(intakes) { intake in
                BarMark(x: .value("日期", intake.timestamp, unit: .day),
                        y: .value("重量", intake.amount))
            }
            if let selectedDate {
                RuleMark(
                    x: .value("Selected", selectedDate, unit: .day)
                )
                .annotation(position: .topLeading) {
                    VStack {
                        Text("Annotation")
                            .font(.caption)
                            .padding(5)
                            .background(RoundedRectangle(cornerRadius: 5).fill(Color.green))
                    }
                }
                .zIndex(-1)
            }
        }
        .chartXSelection(value: $rawSelectedDate)
    }
}

#Preview {
    SimpleAnnotationView()
}```

[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

