---
layout: post
title: "CS193P Lecture05-Properties Layout @ViewBuilder"
date: 2022-10-12 10:35:00
category: programming
tags: [swift, CS193P]
---

### Clean the Code

**EmojiMemoryGame.swift**

```swift
typealias Card = MemoryGame<String>.Card
```


```swift
private(set) var cards: Array<Card>
...

cards = Array<Card>()
```

```swift
cards = []
```

### Computed Property

**MemoryGame.swift**

```swift
private(set) var cards: Array<Card>

private var indexOfTheOneAndOnlyFaceUpCard: Int?
```
may not synced.

```swift
private var indexOfTheOneAndOnlyFaceUpCard: Int? {
   get {
      var faceUpCardIndices = [Int]()
      for index in cards.indices {
         if cards[index].isFaceUp {
            faceUpCardIndices.append(index)
         }
      }
      if faceUpCardIndices.count == 1 {
         return faceUpCardIndices.first
      } else {
         return nil
      }
   }
   set {
      for index in cards.indices {
         if index != newValue {
            cards[index].isFaceUp = false
         } else {
            cards[index].isFaceUp = true
         }
      }
   }
}

mutating func choose(_ card: Card) {
   if let chosenIndex = cards.firstIndex(where: { $0.id == card.id }),
      !cards[chosenIndex].isFaceUp,
      !cards[chosenIndex].isMatched
   {
      if let potentialMatchIndex = indexOfTheOneAndOnlyFaceUpCard {
         if card[chosenIndex].content == cards[potentialMatchIndex].content {
            cards[chosenIndex].isMatched = true
            cards[potentialMatchIndex].isMatched = true
         }
         cards(chosenIndex).isFaceUp = true
      } else {
         indexOfTheOneAndOnlyFaceUpCard = chosenIndex
      }
}
```

#### Take the advantage of functional programing

```swift
private  var indexOfTheOneAndOnlyFaceUpCard: Int? {
   get {
      var faceUpCardIndices = cards.indices.filter({ index in cards[index].isFaceUp })
```

Simplify:  

```swift
private  var indexOfTheOneAndOnlyFaceUpCard: Int? {
   get {
      var faceUpCardIndices = cards.indices.filter({ cards[$0].isFaceUp })
```

#### extension

Simplify to one line: `return faceUpCardIndices.oneAndOnly`

```swift
if faceUpCardIndices.count == 1 {
   return faceUpCardIndices.first
} else {
   return nil
}
```


```swift
extension Array {
   var oneAndOnly:
}
```

Use `Command + Click` on `Array`:  
its **don't care** is `Element`


```swift
extension Array {
   var oneAndOnly: Element {
      if faceUpCardIndices.count == 1 {
         return faceUpCardIndices.first
      } else {
         return nil
      }
   }
}
```

modify:  

```swift
extension Array {
   var oneAndOnly: Element {
      if self.count == 1 {
         return self.first
      } else {
         return nil
      }
   }
}
```

modify again:  

```swift
get {
   let faceUpCardIndices = cards.indices.filter({ cards[$0].isFaceUp })
   return faceUpCardIndices.oneAndOnly
}
```

modify again:  

```swift
get { cards.indices.filter({ cards[$0].isFaceUp }).oneAndOnly }
```

simplify `setter`

```swift
set {
   for index in cards.indices {
      cards[index].isFaceUp = (index == newValue)
   }
}
```


```swift
set {
   cards.indices.forEach({ index in cards[index].isFaceUp = (index == newValue) })
}
```

```swift
set {
   cards.indices.forEach({ cards[$0].isFaceUp = ($0 == newValue) })
}
```

##### trailing closure

```swift
set {
   cards.indices.forEach { cards[$0].isFaceUp = ($0 == newValue) }
}
```

**getter** are also trailing closure, therefore could be ignored.  

```swift
get { cards.indices.filter { cards[$0].isFaceUp }.oneAndOnly }
```

but Prof. prefer to take the result to execute other function:  
(keep `()` when function passed to a function)

```swift
get { cards.indices.filter { cards[$0].isFaceUp }.oneAndOnly }
set { cards.indices.forEach { cards[$0].isFaceUp = ($0 == newValue) } }
```


**Functional Programing** is not noly to reduce lines,  
but also make program more **readable**.

### Property Observers

Swift is able to "detect" when a struct change.



`willSet`  
The syntax can look a lot like a computed var., but it is <u>complete unrelated</u> to that.

```swift
var isFaceUp: Bool {
   willSet {
      if newValue {
         startUsingBonusTime()
      } else {
         stopUsingBonusTime()
      }
   }
}
```

## Layout

How is the space on-screen apportioned to the Views?
It's amazingly simple ...  
1. Container views "offer" space to the Views inside them
2. Views then choose what size they want to be
3. Container Views then position the Views inside of them
4. (and based on that, Container Views choose their own size as per #2 above)


### HStack and VStack
Stacks divide up the space that is offered to them and then offer that to the Views inside.  
It offers space to its "least flexible" (with respect to sizing) subviews first ...

**inflexible** View: `Image`(it wants to be a fixed size; image size).  
**slight more flex** View: `Text` (always wants to size to exactly fit its text).  
**very flexible** View: `RoundedRectangle` (always uses any space offered).

After an offered View(s) takes what it wants, <u>its size is removed from the space available.  Then the stack moves on to the next</u> "least flexible" Views.  
Very flexible views (i.e. those that will take all offered space) will share evenly (mostly).  Rinse and repeat.

#### layoutPriority(Double)
Stack's choice of who to offer space to next can be overridden with `.layoutPriority(Double)`.  
In other words, `layoutPriority` trumps "least flexible".

```swift
HStack {
    Text("Important").layoutPriority(100) // any floating point number is okay
    Image(systemName: "arrow.up")   // the default layout priority is 0
    Text("Unimportant")
}
```

The Important Text above will get the space it wants **first**.  
Then the Image would get its space (since it's less flexible than the Unimportant Text).  
Finally, Unimportant would have to try to fit itself into any remaining space.  
If a Text doesn't get enough space, it will elide (e.g. "Swift is ..." instead of "Swift is great!").  

#### <u>alignment</u> 

When a VStack lays Views out in a column, what if the Views are not all the same width?  
Does it "left align" them?  Or center them?  Or What?  
This is specified via an argument to the stack ...

```swift
VStack(alignment: .leading) { ... }
```

Text baselines can also be used to align:  

```swift
HStack(alignment: .firstTextBaseline) { })
```

### LazyHStack and LazyVStack
1. they don't build the bodies of Views that are not on screen.  
2. they aren't ever flexible  
they don't take up all the space offered to them if they have flexible views inside.  
You'd use these when you have a stack that is in a ScrollView.  

### ScrollView
takes all the space offered to it.  
The views inside it are sized to fit along the axis your scrolling on.


### LazyHGrid and LazyVGrid
We've already seen how these lay out their Views.

### List and Form and OutlineGroup
These are sort of like "really smart VStacks".  
We'll talk about them later in the quarter.

### ZStack
ZStack sizes itself to fit its children.  
If even one of its children is fully flexible size, then the ZStack will be too.  

There are a couple of **alternatives** to using a ZStack:  

### .background modifier
```swift
Text("hello").background(Rectangle().foregroundColor(.red))
```
take a view slide in behind as the background  
This is similar to making a ZStack of this Text and Rectangle (with the Text in front).  
However, there's a big difference in layout between this and using a ZStack to stack them.  
In this case, the resultant View will be <span style="color:red">sized to the Text</span> (the Rectangle is not involved).  
In other words, the Text <span style="color:red">solely determines the layout</span> of this "mini-ZStack to two thing".

### .overlay modifier
Same layout rules as .background, but stacked the other way around.  

will be flexibly sized because Circles are flexibly size even though the Text is not.
```swift
Circle().overlay(Text("Hello"), alignment: .center)
```
This will be <span style="color:red">sized to the Circle</span> (i.e. it will be fully-flexible sized).  
The Text will be stacked on top of the Circle (with the specified alignment inside the Circle).

#### Summary
Background are View modifiers that are kind of acting like *Container Views*.  
This seemed pretty natural, really, because we know that these modifier functions are returning a View and that View that they returned kind of contains the View that they're modifying.  

But some modifiers are actually involved in the layout process.  The most obvious one is .padding.

### Modifiers

Remember that View modifier functions (like .padding) themselves return a View.  
That View, conceptually anyway, "contains" the View it's modifying.  

Many of them just pass the size offered to them along (like .font or .foregroundColor).  
But it possible for a modifier to be involved in the layout process itself.  

For example the View returned by .padding(10) will offer the View that it is modifying a space that is the same size as it was offered, but reduced by 10 points on each side.  

The View returned by .padding(10) would then choose a size for itself which is  
10 points larger on all sides than the View it is modifying ended up chooseing.  

Another example is a modifier we've already used: `.apsectRatio`.

The View returned bye the `.aspectRatio` modifier takes the space offered to it and picks a size for itself that is either smaller (.fit) to respect the ratio or bigger (.fill) to use all the offered space (and more, potentially) and respect the ratio.  
(yes, a View is allowed to choose a size for itself that is larger than the space it was offered!)  


```swift
HStack {	// aside: the default alignment here is .center (not .top, for example)
	ForEach(viewModel.cards) { card in
		CardView(card: card).aspectRatio(2/3, contentMode: .fit)
	}
}
.foregroundColor(Color.orange)
.padding(10)
```
1. the first View here in this is going to be offered space is the .padding(10).
2. .padding(10) View is then going to take that space that was offered to it, subtract 10 on all sides and offer it to the .foregroundColor View.
3. `.foregroundColor` doesn't change space, directly give to `HStack`
4. `HStack` doesn't deal with `CardView`, but .aspectRation Views.
5. `HStack` give space evenly to `.aspectRation` View

Final space is:  




#### Views that take all the space offered to them
Most Views simply size themselves to take up all the space offered to them.  
For example, Shapes usually draw themselves to fit (like RoundedRectangle).  

**Custom Views (like CardView) should do this too whenever sensible.**
But they really should <u>adapt themselves</u> to any space offered to look as good as possible.  
For example, CardView would want to pick a font size that makes its emoji fill the space.  

**Q:** So how does a View know what space was offered to it so it can try to adapt?  
**A:** GeometryReader  

#### GeometryReader
```swift
var body: View {
	GeometryReader { geometry in // using trailing closure syntax for context: parameter
		...
	}
}
```
In other words, GeometryReader's only argument is a @ViewBuiler.

`geometry` is a GeometryProxy:  
```swift
struct GeometryProxy {
	var size: CGSize
	func frame(in: CoordinateSpace) -> CGRect
	var safeAreaInsets: EdgeInsets
}
```

GeometryReader itself (it's just a View) <span style="color:red">always accepts all the Space offered to it.</span>

GeometryReaders always containing fully flexible Views because the GeometryReader itself is always going to accept all the space anyway so it doesn't really matter if the thing inside doesn't accept the space because the space has already been accepted.

```swift
ZStack {
...
}
.edgesIgnoringSafeArea([.top])
```


**EmojiMemoryGameView**  

```swift
struct CardView: View {
	let card: EmojiMemoryGame.Card

	var body: some View {
		GeometryReader { geometry in
			ZStack {
				let shape = RoundedRectangle(cornerRadius: 20)
				if card.isFaceUp {
					shape.fill().foregroundColor(.white)
					shape.strokeBorder(lineWidth: 3)
					Text(card.content).font(Font.system(size: min(geometry.size.width, geometry.size.height) * 0.8))
				}
			}
		}
	}
}
```

Before we move on, I want to talk a little bit about these blue numbers:  

```swift
let shape = RoundedRectangle(cornerRadius: 20)
```

```swift
Text(card.content).font(Font.system(size: min(geometry.size.width, geometry.size.height) * 0.8))
```

We really don't want these blue numbers scattered throughout our code.  We want to collect them all,  
give them good names so that people know what this 20 is and so that they can tweak them.


clean it up:  
you definitely want to do because you want the code, the declarative code in here,  
to be as clean and easy to read as simple as possible.

```swift
...
Text(card.content).font(font(in: geometry.size))
...

private func font(in size: CGSize) -> Font {
	Font.system(size: min(size.width, size.height) * DrawingConstants.fontScale)
}

private struct DrawingConstants {
	static let cornerRadius: CGFloat = 20
	static let lineWidth: CGFloat = 3
	static let fontScale: CGFloat = 0.8
}
```

### @ViewBuilder
What exactly is that argument to ZStack, ForEach, LazyVGrid, etc.?

> Based on a general technology added to Swift to support "list-oriented syntax".  
> It's a simple mechanism for supporting a more convenient syntax for <span style="color:orange">lists of Views</span>.

> Developers can apply it to any of their functions that return something that conforms to View.  
If applied, the function still returns something that conforms to View
But it will do so by interpreting the contents as a <span style="color:orange">list of Views and combines them into one</span>.

> That one View that it combines it into might be a TupleView (for two or more Views).  
> Or it could be a _ConditionalContent View (when there's an if-else in there).  
> Or it could even be EmptyView (if there's nothing at all in there; weird, but allowed).  
> Ant it can be any combination of the above (if's inside other if's, etc.).  

> Note that some of this is not yet fully public API (like _ConditionalContent).  
> But <span style="color:orange">we don't actually care what View it creates</span> for us when it combines the Views in the list.  
> It's always just <span style="color:orange">some View</span> as far as we're concerned.

Bottom line is we don't know what it's going to create and we don't care. In fact, a lot of this is still not even public API like this _ConditionalContent.  
Because we're always just returning some View from these @ViewBuilder things and no matter how complicated that thing is, we don't care what it is.

> Any func or read-only computed var can be marked with <span style="color:orange">@ViewBuilder</span>.  
> If so marked, the contents of that func or var will be interpreted as list of Views.  
> For example, if we wanted to factor out the Views we use to make the front of a Card ...  

```swift
@ViewBuilder
func front(of card: Card) -> some View {
	let shape = RoundedRectangle(cornerRadius: 20)
	shape
	shape.stroke()
	Text(card.content)
}
```

> And it would be legal to put simple if-else's to control which Views are included in the list.  
> (But this is just the front of our card, so we don't need any ifs.)
> The above would return a TupleView<RoundedRectangle, RoundedRectangle, Text>.

just I don't care.  

> That argument's type must be <u>"a function that returns a View"</u>.  
> ZStack, HStack, VStack, ForEach, LazyVGrid, etc. all do this (their content: parameter).  


#### Summary
> `@ViewBuilder` just to reiterate.  
> The contents of a @ViewBuilder is just <u>a list of Views</u>.  
> It's not arbitrary code.  
> <span style="color:orange">if-else</span> (or <span style="color:orange">switch</span> or <span style="color:orange">if let</span>) statements can be used to choose Views to include in the list.  
> You can also have local <span style="color:orange">let</span>s.

Like CardView: 
```swift
let shape = RoundedRectangle()
```
> No other kinds of code is allowed (at least as of the time of this lecture).  






[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


