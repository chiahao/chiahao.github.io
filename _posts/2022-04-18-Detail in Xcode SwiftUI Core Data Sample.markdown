---
layout: post
title: "Detail in Xcode SwiftUI Core Data Sample"
date: 2022-04-18 11:18:00
category: swiftui
tags: [swiftui]
---

```swift
@main
struct SampleCoreDataApp: App {
   let persistenceController = PersistenceController.shared

   var body: some Scene {
      WindowGroup {
         ContentView()
            .environment(\.managedObjectContext, persistenceController.container.viewContext)
      }
   }
}
```

> Summary
>
> Sets the environment value of the specified key path to the given value.
>
> **Declaration**
> ```swift
> func environment<V>(_ keyPath: WritableKeyPath<EnvironmentValues, V>, _ value: V) -> some View
> ```
>
> **Discussion**  
> Use this modifier to set one of the writable properties of the EnvironmentValues structure, including custom values that you create. For example, you can set the value associated with the EnvironmentValues/truncationMode key:
>
> ```swift
> MyView()
>     .environment(\.truncationMode, .head)
> ```
> You then read the value inside MyView or one of its descendants using the Environment property wrapper:
> ```swift
> struct MyView: View {
>     @Environment(\.truncationMode) var truncationMode: Text.TruncationMode
> 
>     var body: some View { ... }
> }
> ```
> SwiftUI provides dedicated view modifiers for setting most environment values, like the View/truncationMode(_:) modifier which sets the EnvironmentValues/truncationMode value:
> ```swift
> MyView()
>     .truncationMode(.head)
> ```
> Prefer the dedicated modifier when available, and offer your own when defining custom environment values, as described in EnvironmentKey.
> The View/environment(_:_:) modifier affects the given view, as well as that view’s descendant views. It has no effect outside the view hierarchy on which you call it.  
>
> ###### Parameters
> |<!---->|<!---->|
> |-|-|
> |keyPath|A key path that indicates the property of the EnvironmentValues structure to update. |
> |value|The new value to set for the item specified by keyPath.|
> ###### Returns
> 
> A view that has the given value set in its environment.


[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


