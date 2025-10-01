---
layout: post
title: "Eliminate data races using Swift Concurrency"
date: 2024-08-02 14:51:00
category: programming
tags: [swift]
---

1. [Eliminate data races using Swift Concurrency](https://developer.apple.com/videos/play/wwdc2022/110351/)
2. [Explore structured concurrency in Swift](https://developer.apple.com/videos/play/wwdc2021/10134)
3. [Beyond the basics of structured concurrency](https://developer.apple.com/videos/play/wwdc2023/10170/)
4. [Swift concurrency: Behind the scenes](https://developer.apple.com/videos/play/wwdc2021/10254)  
Prerequisite talks:  
i. [Meet async/await in Swift](https://developer.apple.com/videos/play/wwdc2021/10132)


## WWDC2021

> drop completion handler
> new async/await syntax

#### old way:

```swift
func fetchThumbnails(
    for ids: [String],
    completion handler: @escaping ([String: UIImage]?, Error?) -> Void
) {
    guard let id = ids.first else { return handler([:], nil) }
    let request = thumbnailURLRequest(for: id)
    let dataTask = URLSession.shared.dataTask(with: request) { data, response, error in
        guard let response = response,
              let data = data
        else {
        	return handler(nil, error)
        }
        // ... check response ...
        UIImage(data: data)?.prepareThumbnail(of: thumbSize) { image in
			guard let image = image else {
				return handler(nil, ThumbnailFailedError())
			}
			fetchThumbnails(for: Array(ids.dropFirst())) { thumbnails, error in
				// ... add image to thumbnails ...
			}
		}
	}
	dataTask.resume()
}
```

> This pattern allows the caller to receive an answer at a later time. As a consequence of that pattern, 
> this function cannot use structured control-flow for error handling. 
> That’s because it only makes sense to handle errors thrown out of a function, not into one.
> Also, this pattern prevents you from using a loop to process each thumbnail. 
> Recursion is required, because the code that runs after the function completes must be nested within the handler.

#### new way:

```swift
func fetchThumbnails(for ids: [String]) async throws -> [String: UIImage] {
	var thumbnails: [String: UIImage] = [:]
	for id in ids {
		let request = thumbnailURLRequest(for: id)
		let (data, response) = try await URLSession.shared.data(for: request)
		try validateResponse(response)
		guard let image = await UIImage(data: data)?.byPreparingThumbnail(ofSize: thumbSize) else {
			throw ThumbnailFailedError()
		}
		thumbnails[id] = image
	}
	return thumbnails
}
```

Use 2 `wait` to show real asynchoronous action happens.


# Task 
1. A task provides a new async context for executing code concurrently
2. Swift checks your usage of tasks to help prevent concurrency bugs
3. When calling an async function a task is not created

# Task forms
## Async-let-binding

```swift
func fetchOneThumbnail(withId id: String) async throws -> UIImage {
	let imageReq = imageRequest(for: id), metadataReq = metadataRequest(for: id)
	let (data, _) = try await URLSession.shared.data(for: imageReq)
	let (metadata, _) = try await URLSession.shared.data(for: metadataReq)
	guard
		let size = parseSize(from: metadata),
		let image = await UIImage(data: data)?.byPreparingThumbnail(ofSize: size)
	else {
		throw ThumbnailFailedError()
	}
	return image
}
```

> Since the downloads are now happening in child tasks, you no longer write "try await" on the right side of the concurrent binding.
> Those effects are only observed by the parent task when using the variables that are concurrently bound.
> So you write "try await" before the expression’s reading the metadata and the image data.
  
> Also, notice that using these concurrently bound variables does not require a method call or any other changes.
> Those variables have the same type that they did in a sequential binding. Now, these child tasks I’ve been talking about are actually part of a hierarchy called a task tree.
  
changed into 

```swift
func fetchOneThumbnail(withId id: String) async throws -> UIImage {
	let imageReq = imageRequest(for: id), metadataReq = metadataRequest(for: id)
	async let (data, _) = URLSession.shared.data(for: imageReq)
	async let (metadata, _) = URLSession.shared.data(for: metadataReq)
	guard
		let size = try await parseSize(from: metadata),
		let image = try await UIImage(data: data)?.byPreparingThumbnail(ofSize: size)
	else {
		throw ThumbnailFailedError()
	}
	return image
}
```

## Cancellation is cooperative

1. Tasks are not stopped immediately when cancelled
2. Cancellation can be checked from anywhere
3. Design your code with cancellation in mind


# Group Task
> offer more flexibility than async-let without giving up all of the nice properties of structured concurrency.

```swift
func fetchThumbnails(for ids: [String]) async throws -> [String: UIImage] {
    var thumbnails: [String: UIImage] = [:]
    try await withThrowingTaskGroup(of: Void.self) { group in
    	for id in ids {
    		thumbnails[id] = try await fetchOneThumbnail(withID: id)
    	}
    }
}
```

> As we saw earlier, async-let works well when there's a fixed amount of concurrency available. Let's consider both functions that I discussed earlier. For each thumbnail ID in the loop, we call fetchOneThumbnail to process it, which creates exactly two child tasks. Even if we in-lined the body of that function into this loop, the amount of concurrency will not change. Async-let is scoped like a variable binding. That means the two child tasks must complete before the next loop iteration begins. But what if we want this loop to kick off tasks to fetch all of the thumbnails concurrently? Then, the amount of concurrency is not known statically because it depends on the number of IDs in the array. The right tool


# Unstructured tasks

```swift
@MainActor
class MyDelegate: UICollectiionViewDelegate {
	func collectionView(_ view: UICollectionView,
						willDisplay call: UICollectionViewCell,
						fowItemAt item: IndexPath) {
		let ids = getThumbnailIds(for: item)
		let thumbnails = await fetchThumbnails(for: ids)
		display(thumbnails, in: cell)
	}
}
```

> However, the delegate method is not async, so we can’t just await a call to an async function. We need to start a task for that, but that task is really an extension of the work we started in response to the delegate action. We want this new task to still run on the main actor with UI priority. We just don’t want to bound the lifetime of the task to the scope of this single delegate method. For situations like this, Swift allows us to construct an unstructured task.

```swift
@MainActor
class MyDelegate: UICollectiionViewDelegate {
	func collectionView(_ view: UICollectionView,
						willDisplay call: UICollectionViewCell,
						fowItemAt item: IndexPath) {
		let ids = getThumbnailIds(for: item)
		Task {
			let thumbnails = await fetchThumbnails(for: ids)
			display(thumbnails, in: cell)
		}
	}
}
```

> Now here’s what happens at runtime. When we reach the point of creating the task, Swift will schedule it to run on the same actor as the originating scope, which is the main actor in this case. Meanwhile, control returns immediately to the caller. The thumbnail task will run on the main thread when there’s an opening to do so without immediately blocking the main thread on the delegate method. Constructing tasks this way gives us a halfway point between structured and unstructured code. A directly constructed task still inherits the actor, if any, of its launched context, and it also inherits the priority and other traits of the origin task, just like a group task or an async-let would. However, the new task is unscoped. Its lifetime is not bound by the scope of where it was launched. The origin doesn’t even need to be async. We can create an unscoped task anywhere. In trade for all of this flexibility, we must also manually manage the things that structured concurrency would have handled automatically. Cancellation and errors won’t automatically propagate, and the task’s result will not be implicitly awaited unless we take explicit action to do so.

1. Inherit actor isolation and priority of the origin context
2. Lifetime is not confined to any scope
3. Can be launched anywhere, even non-async function
4. Must be manually cancelled or awaited

> So we kicked off a task to fetch thumbnails when a collection view item is displayed, and we should also cancel that task if the item is scrolled out of view before the thumbnails are ready. 


> So we kicked off a task to fetch thumbnails when a collection view item is displayed, and we should also cancel that task if the item is scrolled out of view before the thumbnails are ready. Since we’re working with an unscoped task, that cancellation isn’t automatic. Let’s implement it now.

```swift
@MainActor
class MyDelegate: UICollectionViewDelegate {



	func collectionView(_ view: UICollectionView,
						willDisplay cell: UICollectionViewCell,
						forItemAt item: IndexPath) {
		let ids = getThumbnailIDs(for: item)
		Task {
			let thumbnails = await fetchThumbnails(for: ids)
			display(thumbnails, in: cell)
		}
	}
}
```


# Detached Task

```swift
@MainActor
class MyDelegate: UICollectionViewDelegate {
	var thumbnailTasks: [IndexPath: Task<Void, Never>] = [:]

	func collectionView(_view: UICollectionView,
						willDisplay cell: UICollectionViewCell,
						forItemAt item: IndexPath) {
		let ids = getThumbnailIDs(for: item)
		thumbnailTasks[item] = Task {

		}
	}
}
```

```swift
@MainActor

```





[jekyll]: http://jekyllrb.com
[jekyll-gh]: https://github.com/jekyll/jekyll
[jekyll-help]: https://github.com/jekyll/jekyll-help

