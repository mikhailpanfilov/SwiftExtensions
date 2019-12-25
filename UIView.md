[#`Empty view`](https://github.com/mikhailpanfilov/SwiftExtensions/blob/master/UIView.md#empty-view)<br />
[#`Rounded`](https://github.com/mikhailpanfilov/SwiftExtensions/blob/master/UIView.md#rounded)<br />
[#`Is hidden animated`](https://github.com/mikhailpanfilov/SwiftExtensions/blob/master/UIView.md#is-hidden-animated)<br />
[#`Drop shadow`](https://github.com/mikhailpanfilov/SwiftExtensions/blob/master/UIView.md#drop-shadow)<br />
[#`Border view`](https://github.com/mikhailpanfilov/SwiftExtensions/blob/master/UIView.md#border-view)<br />
[#`Snapshot`](https://github.com/mikhailpanfilov/SwiftExtensions/blob/master/UIView.md#snapshot)<br />
[#`Gradient`](https://github.com/mikhailpanfilov/SwiftExtensions/blob/master/UIView.md#gradient)<br />

## [#`Empty view`]()

Returns an empty view. For instance to set as tableView's footer: `tableView.tableFooterView = UIView.emptyView`

```swift
static var emptyView: UIView {
        let view = UIView(frame: CGRect.zero)
        return view
    }
```

## [#`Rounded`]()

Makes view's cornerRadius equals half of `height` or `width`.

```swift
/// Makes view's cornerRadius equals half of `height` or `width`. The default value is by `height`.
    func rounded(byHeight: Bool = true, clipsToBounds: Bool = true) {
        layer.cornerRadius = (byHeight ? bounds.size.height : bounds.size.width) / 2
        self.clipsToBounds = clipsToBounds
    }
```

## [#`Is hidden animated`]()

To allow animation when setting isHidden on any UIView class.

```swift
func isHiddenAnimated(_ isHidden: Bool) {
        if self.isHidden && !isHidden {
            self.alpha = 0.0
            self.isHidden = false
        }
        UIView.animate(withDuration: 0.25, animations: {
            self.alpha = isHidden ? 0.0 : 1.0
        }) { _ in
            self.isHidden = isHidden
        }
    }
```

## [#`Drop shadow`]()

Drop a shadow to any UIView class.

```swift
func dropShadow(color: UIColor, opacity: Float = 0.5, offset: CGSize, radius: CGFloat) {
        self.layer.masksToBounds = false
        self.layer.shadowColor = color.cgColor
        self.layer.shadowOpacity = opacity
        self.layer.shadowOffset = offset
        self.layer.shadowRadius = radius
    }
```

## [#`Border view`]()

Add border to any UIView class.

```swift
func borderView(radius: CGFloat? = nil, border: CGFloat = 1, color: UIColor = .grayBlue) {
        if let radius = radius {
            layer.cornerRadius = radius
        } else {
            layer.cornerRadius = self.frame.height / 2
        }
        layer.borderWidth = border
        layer.borderColor = color.cgColor
        layer.masksToBounds = true
    }
```

## [#`Snapshot`]()

To take a snapshot of any UIView class.

```swift
 var snapshot: UIImage {
        return UIGraphicsImageRenderer(size: bounds.size).image { _ in
            drawHierarchy(in: CGRect(origin: .zero, size: bounds.size), afterScreenUpdates: true)
        }
    }
```

## [#`Gradient`]()

To add a gradient to any UIView class.

```swift
// MARK: Gradient

enum GradientPoint: Int {
    case leftRight
    case rightLeft
    case topBottom
    case bottomTop
    case topLeftBottomRight
    case bottomRightTopLeft
    case topRightBottomLeft
    case bottomLeftTopRight
}

extension UIView {
    func gradientBackground(from color1: UIColor, to color2: UIColor, direction: GradientPoint) {
        let gradient = CAGradientLayer()
        gradient.frame = self.frame
        gradient.colors = [color1.cgColor, color2.cgColor]
        gradient.startPoint = gradientPoint(direction: direction).x
        gradient.endPoint = gradientPoint(direction: direction).y
        layer.insertSublayer(gradient, at: 0)
    }
    
    private func gradientPoint(direction: GradientPoint) -> (x: CGPoint, y: CGPoint) {
        switch direction {
        case .leftRight:
            return (x: CGPoint(x: 0, y: 0.5), y: CGPoint(x: 1, y: 0.5))
        case .rightLeft:
            return (x: CGPoint(x: 1, y: 0.5), y: CGPoint(x: 0, y: 0.5))
        case .topBottom:
            return (x: CGPoint(x: 0.5, y: 0), y: CGPoint(x: 0.5, y: 1))
        case .bottomTop:
            return (x: CGPoint(x: 0.5, y: 1), y: CGPoint(x: 0.5, y: 0))
        case .topLeftBottomRight:
            return (x: CGPoint(x: 0, y: 0), y: CGPoint(x: 1, y: 1))
        case .bottomRightTopLeft:
            return (x: CGPoint(x: 1, y: 1), y: CGPoint(x: 0, y: 0))
        case .topRightBottomLeft:
            return (x: CGPoint(x: 1, y: 0), y: CGPoint(x: 0, y: 1))
        case .bottomLeftTopRight:
            return (x: CGPoint(x: 0, y: 1), y: CGPoint(x: 1, y: 0))
        }
    }
}
```

