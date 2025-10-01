---
layout: post
title: "WWDC2023-Discover Observation in SwiftUI"
date: 2024-08-12 09:34:00
category: programming
tags: [swift]
---

```swift
@Observable class FoodTruckModel {
	var orders: [Order] = []
	var donuts = Donut.all
}


struct DonutMenu: View {
	let model: FoodTruckModel

	var body: some View {
		List {
			Section("Donuts") {
				ForEach(model.donuts) { donut in
					Text(donut.name)
				}
				Button("Add new donut") {
					model.addDonut()
				}
			}
		}
	}
}
```
> if we hange the donuts array by clicking the add donut button, it will invalidate the donut menu view and the UI is updated accordingly.

> say an order is added, the view won't be invalidated becautse the property isn't part of the tracked properties

if we add a computed property to FoodTruckModel: 

```swift
var orderCount: Int { orders.count }
```

and show in another section:

```swift
Section("Orders") {
LabeledContent("Count", value: "\(model.orderCount)")
}
```

> if the orders change, that text will be updated because the orderCount accesses the order's property.


## State, environment and bindable

### @Stat  
When the view needs to have its own state stored in a model.

```swift
struct DonutListView: View {
	var donutList: DonutList
	@State private var donutToAdd: Donut?

	var body: some View {
		List(donutList.donuts) { DonutView(donut: $0) }
		Button("Add Donut") { donutToAdd = Donut() }
			.sheet(item: $donutToAdd) {
				TextField("Name", text: $donutToAdd.name)
				Button("Save") {
					donutList.donuts.append(donutToAdd)
					donutToAdd = nil
				}
				Button("Cancel") { donutToAdd = nil }
			}
	}
}
```

> Here we have the observable model object Donut being used in a sheet presentation.
> When the sheet is presented, the donutToAdd state variable is used to bind values to the editable fields.
> The "donutToAdd" property is managed by the lifetime of the view it's contained in.


### @Environment


```swift
@Observable class Account {
	var userName: String?
}

struct FoodTruckMenuView: View {
	@Environment(Account.self) var account

	var body: some View {
		if let name = account.userName {
			HStack { Text(name); Button("Log out") { account.logOut() } }
		} else {
			Button("Login") { account.showLogin() }
		}
	}
}
```

> Environment lets values be propagated as globally accessible values.
> This lets things be shared in many places. Observable types work fantastically here since the updates created by them are based upon access. When invoking the body of the food truck menu view, the property userName of the account object is accessed. So when the userName will change, the menu view updates. 


### @Bindable

1. Lightweight
2. Connect references to UI
3. Uses $ syntax to create bindings

> The newest of the family of property wrappers is '@Bindable'. The bindable property wrapper is really lightweight. All it does is allow bindings to be created from that type. Getting binding out of a bindable wrapped property is really easy. Just use the $ syntax to get the binding to that property. Most often, this will be bindings to observable types. For the donut view, we have the name being displayed with Text. But in reality, we want to be able to edit that name. So instead of a Text, we can use a TextField. That TextField takes a binding. It reads from the binding to populate the value of the TextField, but it also writes back to the binding when the user changes the value. To make bindings to the donut, all we need to do is use the '@Bindable' property wrapper on the donut property. T


```swift
@Observable class Donut {
	var name: String
}

struct DonutView: View {
	var donut: Donut

	var body: some View {
		Text(donut.name)
	}
}

```

> But in reality, we want to be able to edit that name.

```swift
@Observable class Donut {
	var name: String
}

struct DonutView: View {
	@Bindable var donut: Donut

	var body: some View {
		TextField("Name", text: $donut.name)
	}
}
```

> But in reality, we want to be able to edit that name. So instead of a Text, we can use a TextField. That TextField takes a binding. It reads from the binding to populate the value of the TextField, but it also writes back to the binding when the user changes the value. To make bindings to the donut, all we need to do is use the '@Bindable' property wrapper on the donut property. The property wrapper annotation allows us to use the '$donut.name' syntax and creates a binding when used. 


## SwiftUI property wrappers

> To wrap up the wrappers, there are only three questions you need to answer for using observable models in SwiftUI.

1. Does this model need to be state of the view itself?  
-> @State

2. Does this model need to be part of the global environment of the application?  
-> @Environment

3. Does thie model just need bindings?  
-> @Bindable


> The general rule is for Observable, if a property that is used changes, the view will update.

> This is how Observation synthesizes access to properties normally, except here we've rewritten those custom access points manually so that the non-observable location can be read and store the name. Most of the time, these type of manual cases are not needed, because most of the time, properties of the models in question are composed from other stored properties. But in the rare cases where you need that advanced capability, Observation is flexible enough but easy enough to do on your own. SwiftUI can identify changes in composition since it tracks observable types by access to those properties. This means that if a computed property is composed from other stored properties, then the Observation will just work. However, in the few cases where that's not true, you can use Observation directly to manually add those calls to flag access and mutation. Previously in the Food Truck app, we used ObservableObject to achieve some of the same things we did with the new @Observable 


Before:

```swift
public class FoodTruckModel: ObservableObject {
	@Published public var truck = Truck()

	@Published public var orders: [Order] = []
	@Published public var donuts = Donut.all

	var dailyOrderSummaries: [City.ID: [OrderSummary]] = [:]
	var monthlyOrderSummaries: [City.ID: [OrderSummary]] = [:]
}
```

Use Observable macro:

```swift
@Observable public class FoodTruckModel {
	public var truck = Truck()

	public var orders: [Order] = []
	public var donuts = Donut.all

	var dailyOrderSummaries: [City.ID: [OrderSummary]] = [:]
	var monthlyOrderSummaries: [CIty.ID: [OrderSummary]] = [:]
...
}
```

When it comes to view: 

```swift
struct AccountView: View {
	@ObservedObject var model: FoodTruckModel

	@EnvironmentObject private var accountStore: AccountStore
	@Environment(\.authorizationController) private var authorizationController

	@State private var isSignUpSheetPresented = false
	@State private var isSignOutAlterPresented = false
}
```

After: 

```swift
struct AccountView: View {
	var model: FoodTruckModel

	@Environment(AccountStore.self) private var accountStore
	@Environment(AuthorizationController.self) private var authorizationController

	@State private var isSignUpSheetPresented = false
	@State private var isSignOutAlertPresented = false
}
```





[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

