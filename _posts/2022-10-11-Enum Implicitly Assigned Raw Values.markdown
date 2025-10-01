---
layout: post
title: "Enum Implicitly Assigned Raw Values"
date: 2022-10-11 11:09:00
category: programming
tags: [swift]
---

### Associated Values

```swift
enum productBarcode {
	case upc(Int, Int, Int, Int)
	case qrCode(String)
}

var productBarcode = .qrCode("ABCDEFG")

switch productBarcode {
	case .upc(let numberSystem, let manufacturer, let product, let check):
		print("UPC: \(numberSystem), \(manufacturer), \(product), \(check)")
	
	// if all are variables or costants, place var or let before the case name, for brevity:  
	case let .qrCode(productCode):
		print("QR code: \(productCode)")
}
```


### Raw values are not the same as associated values.  
Raw values are set to prepopulated values when you first define the enumeration in your code.  
The raw value for a particular enumeration case is always the same.

Associated values are set when you create a new constant or variable based on one of the enumeration’s cases, and can be different each time you do so.


```swift
enum Planet: Int {
    case mercury = 1, venus, earth, mars, jupiter, saturn, uranus, neptune
}
```
`Planet.venus` has an **implicit** raw value of 2, and so on.

When strings are used for raw values, the implicit value for each case is the text of that case’s name.

```swift
enum CompassPoint: String {
    case north, south, east, west
}
```
`CompassPoint.south` has an implicit raw value of "south", and so on.

#### `rawValue` property

```swift
let earthsOrder = Planet.earth.rawValue
// earthsOrder is 3

let sunsetDirection = CompassPoint.west.rawValue
// sunsetDirection is "west"
```

```swift
let possiblePlanet = Planet(rawValue: 7)
// possiblePlanet is of type Planet? and equals Planet.uranus
```

[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


