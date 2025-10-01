---
layout: post
title: "Swift Model Container Error"
date: 2024-08-13 07:58:00
category: programming
tags: [swift]
---

```swift
static var sample: () throws -> ModelContainer = {
        let schema = Schema([Account.self, Monster.self])
        let configuration = ModelConfiguration(isStoredInMemoryOnly: true)
        let container = try ModelContainer(for: schema, configurations: [configuration])
        Task { @MainActor in
            Account.insertSampleData(modelContext: container.mainContext)
        }
        return container
    }
```

If didn't specify correct model in `Schema` initializer: 
```swift
Schema([Account.self, Monster.self])
```
There won't be any exception, preview just crash.


[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

