[#`To array`](https://github.com/mikhailpanfilov/SwiftExtensions/blob/master/Sequence.md#to-array)<br/>
[#`To-set`](https://github.com/mikhailpanfilov/SwiftExtensions/blob/master/Sequence.md#to-set)<br/>


## [#`To array`]()

```swift
func toArray() -> [Element] {
        var arr = [Element]()
        forEach { arr.append($0) }
        return arr
    }
```

## [#`To set`]()

```swift
extension Sequence where Element: Hashable {
    func toSet() -> Set<Element> {
        return Set(self)
    }
}
```
