[#`Is not empty`](https://github.com/mikhailpanfilov/SwiftExtensions/blob/master/String.md#is-not-empty)<br/>
[#`Is blank`](https://github.com/mikhailpanfilov/SwiftExtensions/blob/master/String.md#is-blank)<br/>
[#`Localized`](https://github.com/mikhailpanfilov/SwiftExtensions/blob/master/String.md#localized)<br/>
[#`Replace at with`](https://github.com/mikhailpanfilov/SwiftExtensions/blob/master/String.md#replace-at-with)<br/>
[#`Attributed`](https://github.com/mikhailpanfilov/SwiftExtensions/blob/master/String.md#attributed)<br/>
[#`Height for width and font`](https://github.com/mikhailpanfilov/SwiftExtensions/blob/master/String.md#height-for-width-and-font)<br/>
[#`Trimmed`](https://github.com/mikhailpanfilov/SwiftExtensions/blob/master/String.md#trimmed)<br/>
[#`Numeric`](https://github.com/mikhailpanfilov/SwiftExtensions/blob/master/String.md#numeric)<br/>
[#`isNumeric`](https://github.com/mikhailpanfilov/SwiftExtensions/blob/master/String.md#isnumeric)<br/>
[#`Capitalize first letter`](https://github.com/mikhailpanfilov/SwiftExtensions/blob/master/String.md#capitalize-first-letter)<br/>
[#`Random letter`](https://github.com/mikhailpanfilov/SwiftExtensions/blob/master/String.md#random-letter)<br/>
[#`Random character`](https://github.com/mikhailpanfilov/SwiftExtensions/blob/master/String.md#random-character)<br/>[#`Take`](https://github.com/mikhailpanfilov/SwiftExtensions/blob/master/String.md#take)<br/>
[#`Removed last`](https://github.com/mikhailpanfilov/SwiftExtensions/blob/master/String.md#removed-last)<br/>
[#`Words array`](https://github.com/mikhailpanfilov/SwiftExtensions/blob/master/String.md#words-array)<br/>
[#`Size`](https://github.com/mikhailpanfilov/SwiftExtensions/blob/master/String.md#size)<br/>
[#`Is valid url`](https://github.com/mikhailpanfilov/SwiftExtensions/blob/master/String.md#is-valid-url)<br/>



## [#`Is not empty`]()

Sometimes it's way more readable.

```swift
var isNotEmpty: Bool {
        return !isEmpty
    }
```

## [#`Is blank`]()

Checks if [trimmed](https://github.com/mikhailpanfilov/SwiftExtensions/blob/master/String.md#trimmed) string is empty.

```swift
var isBlank: Bool {
        return trimmed().isEmpty
    }
```

## [#`Localized`]()

Example: `title = "your_screen_title".localized`. You should have a value under this key in your `Localizable.strings` file(`"your_screen_title" = "Swift extensions";`)

```swift
var localized: String {
        return NSLocalizedString(self, comment: "")
    }
    
    func localized(_ args: CVarArg...) -> String {
        return String(format: self.localized, locale: Locale.current, arguments: args)
    }
```

## [#`Replace at with`]()

Replaces character at index.

```swift
func replace(at index: Int, with newChar: Character) -> String {
        var chars = Array(self)
        chars[index] = newChar
        let modifiedString = String(chars)
        return modifiedString
    }
```

## [#`Attributed`]()

To easily set attributes.

```swift
func attributed(size: CGFloat = 17.0,
                    letterSpacing: CGFloat = 1.6,
                    weight: UIFont.Weight = .regular,
                    lineSpacing: CGFloat? = nil) -> NSAttributedString {
        let attributedString = NSMutableAttributedString(string: self, attributes: [
            .font: UIFont.systemFont(ofSize: size, weight: weight),
            .kern: letterSpacing
        ])
        if let lineSpacing = lineSpacing {
            let paragraphStyle = NSMutableParagraphStyle()
            paragraphStyle.lineSpacing = lineSpacing
            paragraphStyle.alignment = .center
            attributedString.addAttribute(NSAttributedString.Key.paragraphStyle, value: paragraphStyle, range: NSMakeRange(0, attributedString.length))
        }
        return attributedString
    }
```

## [#`Height for width and font`]()

Counts height depending on width and font.

```swift
func height(width: CGFloat, font: UIFont) -> CGFloat {
        let constraintRect = CGSize(width: width, height: .greatestFiniteMagnitude)
        let boundingBox = self.boundingRect(with: constraintRect,
                                            options: .usesLineFragmentOrigin,
                                            attributes: [NSAttributedString.Key.font: font],
                                            context: nil)
        return ceil(boundingBox.height)
    }
```

## [#`Trimmed`]()

Returns a new string made by removing from both ends of the String characters contained in a given character set.

```swift
func trimmed(_ charSet: CharacterSet = CharacterSet.whitespacesAndNewlines) -> String {
        return self.trimmingCharacters(in: charSet)
    }
```

## [#`Numeric`]()

Remove all non-numeric characters from a string

```swift
var numeric: String {
    return self.components(separatedBy: CharacterSet(charactersIn: ".0123456789").inverted).joined(separator: "")
}
```

## [#`isNumeric`]()

Check if string contains only numbers

```swift
var isNumeric: Bool {
    guard !self.isEmpty else { return false }
    let nums: Set<Character> = [".", "0", "1", "2", "3", "4", "5", "6", "7", "8", "9"]
    return Set(self).isSubset(of: nums)
}
```

## [#`Capitalize first letter`]()

Returns the same text, capitalizing the first letter.

```swift
func capitalizingFirstLetter() -> String {
        return prefix(1).uppercased() + dropFirst()
    }
    
    mutating func capitalizeFirstLetter() {
        self = self.capitalizingFirstLetter()
    }
```

## [#`Random letter`]()

Returns random letter.

```swift
static var randomLetter: String {
        let characters : String = "abcdefghijklmnopqrstuvwxyz"
        let randomIndex = characters.index(characters.startIndex, offsetBy: Int(arc4random_uniform(UInt32(characters.count))))
        return String(characters[randomIndex])
    }
```

## [#`Random character`]()

Returns random character. Might be uppercased.

```swift
static func randomCharacter(uppercased: Bool = false) -> Character {
        let characters: String = uppercased ? "abcdefghijklmnopqrstuvwxyz".uppercased() : "abcdefghijklmnopqrstuvwxyz"
        let randomIndex = characters.index(characters.startIndex, offsetBy: Int(arc4random_uniform(UInt32(characters.count))))
        return characters[randomIndex]
    }
```

## [#`Take`]()

Takes elements from the beginning. `"0123456789".take(3) | Result: 012`

```swift
func take(_ offset: Int) -> String {
        let offset = self.index(self.startIndex, offsetBy: min(self.count, offset))
        return String(self[..<offset])
    }
```

## [#`Removed last`]()

`"0123456789".removedLast(3) | Result: 0123456`

```swift
func removedLast(_ offset: Int) -> String {
        guard let offset = self.index(endIndex, offsetBy: -offset, limitedBy: startIndex) else { return "" }
        return String(self[..<offset])
    }
```

## [#`Words array`]()

Creates array of words separated by space.

```swift
var wordsArray: [String] {
        return self.components(separatedBy: " ").filter { !$0.isEmpty }
    }
```

## [#`Size`]()

Returns the bounding box size the receiver occupies when drawn with the given attributes.

```swift
func size(_ font: UIFont) -> CGSize {
        let fontAttributes = [NSAttributedString.Key.font: font]
        return self.size(withAttributes: fontAttributes)
    }
```

## [#`Is valid url`]()

Checks if valid url.

```swift
var isValidUrl: Bool {
        guard let url = URL(string: self) else { return false }
        return url.scheme == "http" || url.scheme == "https"
    }
```

## [#`Is valid email`]()

Checks if valid email.

```swift
var isValidEmail: Bool {
        let emailRegEx = "[A-Z0-9a-z._%+-]+@[A-Za-z0-9.-]+\\.[A-Za-z]{2,64}"
        let emailTest = NSPredicate(format:"SELF MATCHES %@", emailRegEx)
        return emailTest.evaluate(with: self)
    }
```



