[#`Name Describable` (identifier, typeName)](https://github.com/mikhailpanfilov/SwiftExtensions/blob/master/Protocols.md#name-describable-identifier-typeName)<br />

## [#`Name Describable` (identifier, typeName)]()

A way to get a `typeName` or `identifier`. A common case to use while initializing `NameTableViewCell.identifier`.

```swift
protocol NameDescribable { }
extension NameDescribable {
    var typeName: String {
        return String(describing: type(of: self))
    }
    
    static var identifier: String {
        return String(describing: self)
    }
}

extension NSObject: NameDescribable { }
```

