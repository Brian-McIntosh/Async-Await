# Async-Await

Let's Build That App: https://www.youtube.com/watch?v=bxCDL3kY8XA&t=1691s

* Arrived in Swift 5.5 during WWDC 2021
* Can simplify our code with async-await and make our asynchronous code easier to read

What is **async**?

#### Easier JSON Fetching; alternative to closures and Combine
```swift
func fetchImages() async throws -> [UIImage] {
    // .. perform data request
}
```

The above method would have been written as followed:
```swift
func fetchImages(completion: (Result<[UIImage], Error>) -> Void) {
    // .. perform data request
}
```

Completion closure downsides:
1. You have to make sure you call the completion closure in each possible method exit
2. Harder to read
3. Retain cycles need to be avoided using weak references

What is **await**?
One will never go without the other. *"Await is awaiting a callback from his buddy async."*

Calling our earlier defined async throwing fetch images method:
```swift
do {
    let images = try await fetchImages()
    print("Fetched \(images.count) images.")
} catch {
    print("Fetching images failed with error \(error)")
}
```
It might be hard to believe, but the above code example is performing an asynchronous task.







