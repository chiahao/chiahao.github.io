---
layout: post
title: "CS193P Lecture06-Protocols Shape"
date: 2022-10-12 10:35:00
category: programming
tags: [swift, CS193P]
---

### protocol

protocol inheritance

```swift
protocol Moveable {
}

protocol Vehicle: Movable {
}

class Car: Vehicle {
	// 要實作 Movable、Vehicle
}
```

> <u>Very rarely</u>, a protocol can be used as a type (in any other circumstance a type can be used).  
> Not all protocols can be used this way (View can't, nor Equatable, nor Identifiable).  

doesn't work with View、Equatable or Identifiable  

```swift
func travelAround(using moveable: Moveable)
let foo = [Moveable]
```

**最好不要直接用作 type**  

會用到的 protocol:  Hashable, Identifiable, CustomStringConvertible ...

ObservableObject 比較特別, 會免費幫我們實作 objectWillChange  


> We can also use protocols to restrict an extension to work only with certain things.  

```swift
extension Array where Element: Hashable { ... }
```

> We can also use protocols to restrict <u>individual functions</u> to work only with certain things.  

```swift
init(data: Data) where Data: Collection, Data.Element: Identifiable
```

protocol 不只可以用來限制東西, 

> Occasionally a protocol is used to set up an agreement between two entities.  
> Example: `DropDelegate`
> The system lets any struct/class that conforms to `DropDelegate` participate in drag & drop.  
> The `DropDelegate` protocol makes it clear to that data structure what its responsibilities are   
> (i.e. the data structure must implement the funcs/vars in the `DropDelegate` protocol).


#### code sharing

<span style="color:red">Implementation can be added to a protocol by creating an extension to it</span>

這是 Views 的 foregroundColor, font, ... 等的實作方式

> An <span style="color:purple">extension</span> can also add a <u>default</u> implementation for a func or var in the protocol.  
> (That's how ObservableObjects get objectwillChange for free.)



#### One way to think about protocols is <u>contrains and gains</u>

```swift
protocol Equatable {
	static func ==(lhs: Self, rhs: Self) -> Bool
}
```

因為有用到 Self, 所以不能寫  

That's why these kinds of Self-referencing protocols cannot be used as just a normal type inside of Array.

```swift
var x: [Equatable]
```

struct 裡的 property 如果都是 Equatable, 那這個 struct conform to Equatable 時, 就不用實作 func

沒有要求要加 extension 到 protocol,  
那是 Apple 在做的,  
只是要知道怎麼做而已。



#### Back to demo
和台大老師一樣, 也是先畫靶再畫箭!

Create View combiner that kept all the cards the right size to fit them all on screen with a certain aspect ratio.  

想像如果這樣的 View combiner 存在的話, 那原本的:  

```swift
// ScrollView {
// 	LazyVGrid(columns: [GridItem(.adaptive(minimum: 100))]) {
// 		ForEach(game.cards) { card in
			// 只留下裡面的:  
			CardView(card: card)
				.aspectRatio(2/3, contentMode: .fit)
				.onTapGesture {
					game.choose(card)
				}
// 		}
// 	}
// }
```

然後叫做 AspectVGrid, 然後再想應該要有什麼參數:
1. items
2. aspectRatio: 要維持卡片比例
3. content: return view,  
just like ForEach gave me the card back

```swift
AspectVGrid(items: game.cards, aspectRatio: 2/3, content: { card in
	CardView(...)
	...
})
```

再來實作 AspectVGrid
1. 先處理 argument
```swift
var items: ...
// Everything we do with drawing is `CGFloat`.
var aspectRatio: CGFloat
var content: ...
```
2. 再來決定 argument 的 type
```swift
var items: [Item]
```
因為是 don't care, 所以就必須在 struct 的宣告加上 `<>`  
just to let the world know this has a "don't care" in it called Item.

```swift
struct AspectVGrid<Item>: View {
	var items: [Item]
}
```

那 content 呢? 可能會覺得是回傳 View, 但**不行**!  
因為 View 是 protocol, 是 contraints and gains thing, and   
Self-referential.

```swift
// Not work!
var content: (Item) -> View
```
那 `some View` 呢?  
因為 `some View` means  
> go look in here see what this is and replace `some View` whatever you find.

但是 compiler 無法這時知道 content 裡面有什麼  
對照原本的程式, 其實  

```swift
CardView(...)
...
```

是個 don't care, 可以是 Rectangle, card, or ZStack, 所以  

```swift
struct AspectVGrid<Item, ItemView>
...
	
	var content: (Item) -> ItemView
```

但其實 don't care that it's a View

```swift
struct AspectVGrid<Item, ItemView> where ItemView: View
...
	var content: (Item) -> ItemView
```

AspectVGrid 其實是個 LazyVGrid, 所以從 LazyVGrid 開始寫:  

```swift
var body: some View {
	let width: CGFloat = 100
	LazyVGrid(columns: [GridItem(.adative(minimum: width))]) {
		ForEach(items) {item in
			content(item).aspectRatio(aspectRatio, contentMode: .fit)
		}
	}
}
```

這時有個錯誤:  
"Referencing initializer on 'ForEach' requires that 'item' conform to 'Identifiable'"  

```swift
sturct AspectVGrid<Item, ItemView>: View where ItemView: View, Item: Identifiable {
```

老師的程式做了一點簡化:  沒有 spacing  

```swift
var body: some View {
	GeometryReader: { geometry in
		let width: CGFloat = widthThatFits(itemCount: items.count, in: geometry.size, itemAspectRatio: aspectRatio)
		LazyVGrid(columns: [adaptiveGridItem(width: width)], spacing: 0) {
			...
		}
	}
}
```

#### Flexible
目前 GeometryReader 不是 flexible, 因為 LazyVGrid 不是 flexible.  
因為 LazyVGrid sizes itself to its items.  

**Just as a matter of good habit, I like to make sure that the things in my GeometryReader are flexible in size.**

```swift
VStack {
	// 把 LazyVGrid 放進來
	// 加再上 Spacer()
	// 因為加入了 flexible 的 Spacer, 就會讓 VStack 變 flexible
	Spacer(minLength: 0)
}
```

#### 引入 @ViewBuilder
這邊有點為了教學而引用.  
e.g. 把翻牌的程式不要放在 CardView 裡, 而是放在 AspectVGrid 的呼叫:  
```swift
AspectVGrid(items: game.cards, aspectRatio: 2/3, content: { card in
	if card.isMatched && !card.isFaceUp {
		Rectangle().opacity(0)
	} else {
		CardView(...)
		...
	}
})
```
會得到改寫的地方沒有 conform to View.  
是因為真的不是 View, 而且也不是 well-formed function.  
解法: 到 AspectVGrid 加 `init()`:  

```swift
init(items: [Item], aspectRatio: CGFloat, content: (Item) -> ItemView) {
	self.items = items
	self.aspectRatio = aspectRatio
	self.content = content
}
```

會得到錯誤: "Assigning non-escaping parameter 'context' to an @escaping closure"  
是因為傳入的 content 跳脫了這個 init 的 context, 而在後面被使用:  

```swift
init(items: [Item], aspectRatio: CGFloat, content: @escaping (Item) -> ItemView) {
```

1. So people who are calling your initializer here know oh he's going to hold onto this function.  
2. compiler 須要知道它是 escaping, 才會 create memory for it, 否則可能 execute inline.  
Because functions are types just like a struct, and that structs and enums are value types, they don't live in heap.  
Clsure's function types are reference types.  They actually live in the heap and are pointed to. 

然後再加上 @ViewBuilder 就好:  
```swift
init(items: [Item], aspectRatio: CGFloat, @ViewBuilder content: @escaping (Item) -> ItemView) {
```

#### @ViewBuilder 加在 func 上
可能覺得傳入 AspectVGrid 的東西太長, 所以切成另一個 func:  

**EmojiMemoryGameView**  

```swift
AspectVGrid(items: game.cards, aspectRatio: 2/3, content: { card in
	cardView(for: card)
})
...
@ViewBuilder
private func cardView(for card: EmojiMemoryGame.Card) -> some View {
	if card.isMatched && !card.isFaceUp {
		Recatngle().opacity(0)
	} else {
		CardView(...)
		...
	}
}
```

加上 @ViewBuilder 後, 才會告訴 swift, 我們要用 @ViewBuilder syntax.  

老師比較傾向放在 inline, 而不是切成另一個 function.  



### Shape

> Shape is a protocol that inherits from View.  
> In other words, all Shapes are also Views.  

function can take don't care:  

```swift
func fill<S>(_ whatToFillWith: S) -> some View where S: ShapeStyle
```
This is a <u>generic function</u>


希望第一張牌一直是翻面的:  
```swift
struct ContentView_Previews: PreviewProvider {
	static var previews: some View {
		let game = EmojiMemoryGame()
		game.choose(game.cards.first!)
		return EmojiMemoryGameView(game: game)
	}
}
```


Can kind of think of the way paths draw as you're drawing with a pen,  
and you can lift the pen up and move it or you can leave the pen down and add lines and arcs.  





[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help


