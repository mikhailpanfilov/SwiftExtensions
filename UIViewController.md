[#`Instantiate controller`](https://github.com/mikhailpanfilov/SwiftExtensions/blob/master/UIViewController.md#instantiate-controller)<br/>
[#`Hide keyboard`](https://github.com/mikhailpanfilov/SwiftExtensions/blob/master/UIViewController.md#hide-keyboard)<br/>

## [#`Instantiate controller`]()

That makes your code clean and simple. Instantiation from a [storyboard](https://github.com/mikhailpanfilov/SwiftExtensions/blob/master/Enums.md#storyboard) by the controller's [identifier](https://github.com/mikhailpanfilov/SwiftExtensions/blob/master/Protocols.md#name-describable-identifier-typeName) takes just one line.
Example:
```swift
let viewController = YourViewController.from(storyboard: .main)
```
```swift
private class func instantiateControllerInStoryboard<T: UIViewController>(_ storyboard: UIStoryboard, identifier: String) -> T {
        return storyboard.instantiateViewController(withIdentifier: identifier) as! T
    }
    private class func controllerInStoryboard(_ storyboard: UIStoryboard, identifier: String) -> Self {
        return instantiateControllerInStoryboard(storyboard, identifier: identifier)
    }
    class func from(storyboard: Storyboard) -> Self {
        return controllerInStoryboard(UIStoryboard(name: storyboard.rawValue, bundle: nil), identifier: identifier)
    }
}
```

## [#`Hide keyboard`]()

Close keyboard by touching anywhere

```swift
func hideKeyboardWhenTappedAround() {
        let tap: UITapGestureRecognizer = UITapGestureRecognizer(target: self, action: #selector(UIViewController.dismissKeyboard))
        tap.cancelsTouchesInView = false
        view.addGestureRecognizer(tap)
    }
    @objc func dismissKeyboard() {
        view.endEditing(true)
    }
```
