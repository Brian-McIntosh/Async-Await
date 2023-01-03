# Async-Await
* Arrived in Swift 5.5 during WWDC 2021
* Can simplify our code and make code easier to read
* An alternative to closures and Combine

## Bottom Line:
It replaces code like this:
```swift
func getAllToDos(url: URL, completion: @escaping (Result<[ToDo], NetworkError>) -> Void) {
    URLSession.shared.dataTask(with: url) { data, response, error in
        guard let data = data, error == nil,
              (response as? HTTPURLResponse)?.statusCode == 200 else {
                completion(.failure(.badRequest))
                return
               }
        let todos = try? JSONDecoder().decode([ToDo].self, from: data)
        completion(.success(todos ?? []))
    }.resume()
}
```
Closure Completion Downsides:
1. You have to make sure you call the completion closure in each possible method exit
2. Harder to read
3. Retain cycles need to be avoided using weak references

## async
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







