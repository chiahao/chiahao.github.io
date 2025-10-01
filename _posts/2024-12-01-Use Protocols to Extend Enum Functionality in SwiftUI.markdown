---
layout: post
title: "Use Protocols to Extend Enum Functionality in SwiftUI"
date: 2024-12-01 11:23:00
category: program
tags: [swift]
---

```swift
import Foundation
import SwiftUI

enum DayPhase: String, Codable, CustomStringConvertible, CaseIterable, ColorProvidable {
    case morning
    case night
    
    var description: String {
        switch self {
        case .morning: "早上"
        case .night: "晚上"
        }
    }
    
    public var image: String {
        switch self {
        case .morning: "sun"
        case .night: "moon"
        }
    }
    
    public func backgroundColor() -> Color {
        switch self {
        case .morning: Color(red: 242/255, green: 201/255, blue: 0)
        case .night: Color(red: 122/255, green: 125/255, blue: 170/255)
        }
    }
}

```


```swift
import Foundation
import SwiftUI  

struct OptionToggleView<T: CaseIterable & Hashable & CustomStringConvertible & ColorProvidable>: View where T.AllCases: RandomAccessCollection {
    @ObservedObject var viewModel: OptionToggleViewModel<T>
    let imageForOption: (T) -> String
    
    var body: some View {
        HStack {
            ForEach(T.allCases, id: \.self) { option in
                Button(action: {
                    viewModel.selectedOption = option
                }) {
                    Image(imageForOption(option))
                        .resizable()
                        .frame(width: 30, height: 30)
                        .padding(1)
                    Text(option.description)
                        .padding([.trailing], 8)
                }
                .background(
                    viewModel.selectedOption == option ? option.color() : Color.clear
                )
                .foregroundColor(
                    viewModel.selectedOption == option ? option.color() : Color.clear
                )
                .cornerRadius(5)
            }
        }
    }
}
```



[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

