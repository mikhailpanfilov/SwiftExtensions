[#`Set title`](https://github.com/mikhailpanfilov/SwiftExtensions/blob/master/UIButton.md#set-title)<br />
[#`Set image`](https://github.com/mikhailpanfilov/SwiftExtensions/blob/master/UIButton.md#set-image)<br />
[#`Set title color`](https://github.com/mikhailpanfilov/SwiftExtensions/blob/master/UIButton.md#set-title-color)<br />
[#`Set image animated`](https://github.com/mikhailpanfilov/SwiftExtensions/blob/master/UIButton.md#set-image-animated)<br />
[#`Underline title`](https://github.com/mikhailpanfilov/SwiftExtensions/blob/master/UIButton.md#underline-title)<br />
[#`Phone's button title`](https://github.com/mikhailpanfilov/SwiftExtensions/blob/master/UIButton.md#phones-button-title)<br />

## [#`Set title`]()

Since most of the time, I set a title for `.normal`, it's easier to use:

```swift
func set(title: String) {
        setTitle(title, for: .normal)
    }
```

## [#`Set image`]()

Since most of the time, I set an image for `.normal`, it's easier to use:

```swift
func set(image: UIImage) {
        setImage(image, for: .normal)
    }
```

## [#`Set title color`]()

To set title's color

```swift
func set(titleColor: UIColor) {
        setTitleColor(titleColor, for: .normal)
    }
```

## [#`Set image animated`]()

To set image animated

```swift
func set(image: UIImage?, for state: UIControl.State = .normal, animated: Bool) {
        let animationDuration: TimeInterval = animated ? 0.25 : 0
        UIView.transition(with: self, duration: animationDuration, options: .transitionCrossDissolve, animations: {
            self.setImage(image, for: state)
        }, completion: nil)
    }
```

## [#`Underline title`]()

To make the button's title underlined using its font and color.

```swift
func underlineText(animated: Bool = false) {
        guard let title = title(for: .normal), let font = titleLabel?.font, let titleColor = titleColor(for: .normal) else {
            return 
        }
        let attributedString = NSMutableAttributedString(string: title)
        attributedString.setAttributes([.font: font, .foregroundColor: titleColor, .underlineStyle: 1],range: NSRange.init(location: 0, length: attributedString.length))
        if !animated {
            UIView.performWithoutAnimation {
                setAttributedTitle(attributedString, for: .normal)
                layoutIfNeeded()
            }
        } else {
            setAttributedTitle(attributedString, for: .normal)
        }
    }
```

## [#`Phone's button title`]()

To make the button's title the same as cell phones'.

```swift
func phonesButtonTitle(at index: Int) {
        let buttonsTitles = ["0\n   ", "1\n   ", "2\nABC", "3\nDEF", "4\nGHI", "5\nJKL", "6\nMNO", "7\nPQRS", "8\nTUV", "9\nWXYZ"]
        
        let attributedString = NSMutableAttributedString(string: buttonsTitles[index])
        
        let attributes0: [NSAttributedString.Key : Any] = [
            .foregroundColor: UIColor.darkText,
            .font: UIFont.systemFont(ofSize: 36)
        ]
        attributedString.addAttributes(attributes0, range: NSRange(location: 0, length: 1))
        
        let attributes1: [NSAttributedString.Key : Any] = [
            .foregroundColor: UIColor.darkText,
            .font: UIFont.systemFont(ofSize: 10)
        ]
        attributedString.addAttributes(attributes1, range: NSRange(location: 2, length: attributedString.string.count - 2))

        setAttributedTitle(attributedString, for: .normal)
    }
```
