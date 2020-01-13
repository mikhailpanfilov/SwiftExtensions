[#`Scroll while dragging on button`](https://github.com/mikhailpanfilov/SwiftExtensions/blob/master/UISctollView.md#scroll-while-dragging-on-button)<br />


## [#`Scroll while dragging on button`]()

ScrollView starts scrolling when dragging on buttons

```swift
class UIButtonScrollView: UIScrollView {

    override func touchesShouldCancel(in view: UIView) -> Bool {
        if view.isKind(of: UIButton.self) {
          return true
        }

        return super.touchesShouldCancel(in: view)
    }    
}
```
