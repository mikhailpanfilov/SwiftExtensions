[#`Storyboard`](https://github.com/mikhailpanfilov/SwiftExtensions/blob/master/Enums.md#storyboard)<br />
[#`Decimal Points`](https://github.com/mikhailpanfilov/SwiftExtensions/blob/master/Enums.md#decimal-points)<br />


## [#`Storyboard`]()

To group all of your storyboards to make view controller's [instantiation](https://github.com/mikhailpanfilov/SwiftExtensions/blob/master/UIViewController.md#instantiate-controller) simpler.

```swift
enum Storyboard: String {
    case main = "Main"
}
```

## [#`Decimal Points`]()

For instance to get rounded string: `String(format: DecimalPoints.one.format, 123.123)`

```swift
enum DecimalPoints {
    case zero, one, two, three, ridiculous
    var format: String {
        switch self {
        case .zero: return "%.0f"
        case .one: return "%.1f"
        case .two: return "%.2f"
        case .three: return "%.3f"
        case .ridiculous: return "%f"
        }
    }
}
```
