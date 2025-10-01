---
layout: post
title: "Swift Create Array From 1 to N"
date: 2022-02-15 09:39:00
category: program
tags: [swift]
---


```swift
// create an empty Int array
var arr = [Int]()
// extend the array using a Range    
arr += 1...100

var arr30 = Array(1...30)

// even array
var arr40 = Array(1...40)
print(arr40[arr40.partition{$0 % 2 == 0}...])

print(Array(stride(from: 0, to: 40, by: 2)))
```




[Swift: Create an array of numbers 1 to 100 and divide into odds and evens using partition()](https://coderwall.com/p/vogzvq/swift-create-an-array-of-numbers-1-to-100-and-divide-into-odds-and-evens-using-partition)  
**P.S.** 好像是舊版的 swift 才有這個方法
```swift
// partition based on the use of odd or even numbers
let idx = partition(&arr, indices(arr)) { i, _ in i%2==0 }
// use the returned point of partition (index) to split the array into odd and even
arr[0..<idx] // even
arr[idx..<arr.endIndex] // odd
```

[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

