[#`Remove element`](https://github.com/mikhailpanfilov/SwiftExtensions/blob/master/Array.md#remove-element)<br/>
[#`Last index`](https://github.com/mikhailpanfilov/SwiftExtensions/blob/master/Array.md#last-index)<br/>
[#`Last index with predicate`](https://github.com/mikhailpanfilov/SwiftExtensions/blob/master/Array.md#last-index-with-predicate)<br/>
[#`Last index of an Element`](https://github.com/mikhailpanfilov/SwiftExtensions/blob/master/Array.md#last-index-of-an-element)<br/>
[#`Is not empty`](https://github.com/mikhailpanfilov/SwiftExtensions/blob/master/Array.md#is-not-empty)<br/>

## [#`Remove element`]()

This is extension for `Array where Element: Equatable`

```swift
extension Array where Element: Equatable {
    mutating func remove (element: Element) {
        if let i = self.index(of: element) {
            self.remove(at: i)
        }
    }
}
```

## [#`Last index`]()

```swift
var lastIndex: Int {
        return count - 1
    }
```

## [#`Last index with predicate`]()

Example: `yourArray.lastIndex(where: { $0 == "Swift" })`

```swift
func lastIndex(where predicate: (Element) throws -> Bool) rethrows -> Int? {
        for i in (0..<count).reversed() {
            if try predicate(self[i]) {
                return i
            }
        }
        return nil
    }
```

## [#`Last index of an Element`]()

This is extension for `Array where Element: Equatable`

```swift
extension Array where Element: Equatable {
    func lastIndex(of element: Element) -> Int? {
        for i in (0..<count).reversed() {
            if element == self[i] {
                return i
            }
        }
        return nil
    }
}
```

## [#`Is not empty`]()

```swift
var isNotEmpty: Bool {
        return !isEmpty
    }
```
