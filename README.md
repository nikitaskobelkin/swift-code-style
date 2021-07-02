# Skobelkin's code style
[![Version](https://img.shields.io/badge/VERSION-BETA-1abc9c.svg)](https://github.com/nikitaskobelkin/swift-code-style)

My principles of coding style in my projects for me and my friends.

1. [General](#general)
2. [Naming](#naming)
3. [Structure](#structure)
4. [Class (Struct) Structure](#class-structure)
5. [Protocols](#protocols)
6. [Types](#types)
7. [Forced Unwrapping](#forced-unwrapping)
8. [Forced Casting](#forced-casting)
9. [Enum Cases](#enum-cases)
10. [Spacing](#spacing)
11. [Magic Numbers](#magic-numbers)
12. [Comments (MARK)](#comments)

## General
- Global constants are not allowed, they must always be inside the namespace.
- Compiler warnings are considered bugs and are not allowed. Exception: TODO :, FIXME:
- Follow the typing rules (even in comments).

🥰
```
// A comment that someone left (for example, I), here we will put an end.
```
🤮
```
// a comment that someone left ( for example, I) , here we will put an end .
```

## Naming
- Variable names must describe a variable semantically (the meaning of transferring it), variables of the form a or x are not allowed.
- Abbreviations (e.g. res) should be avoided unless they are generally accepted (e.g. url).
- CamelCase is used, not snake_case.

### For Variables And Functions
> Beginning with lowercase.

### For Classes, Protocols, Structures, Enums, etc.
> Beginning with uppercase.

🥰
```swift
class Weather {
  var cityName: String
  var cloudy: String
}
```
🤮
```swift
class weather {
  var City_NAME: String
  var cldly: String
}
```

## Structure
- Tab is used for identification (not spaces).
- Functions, loops and other expressions (if, else, switch, while, etc.) must have an opening curly brace on the same line as the expression. The closing one is always on a new line.
- There must be exactly one space between the construct and the opening curly brace.
- Function call parentheses are not separated from it by a single space.
- Function parameter parentheses are separated by one space from the name.
- There should be exactly one blank line between functions, for readability and code organization.

🥰
```swift
func checSpaces {
  if spaces.count > 8 {
    print("Good")
  } else {
    print("Good too")
  }
}

func welcome () {
  print("Welcome!")
}
```
🤮
```swift
func checSpaces(_ spaces: [String]) {
  if spaces.count > 8{
    print("Bad")
  }
  else {
    print("Bad too")}
}
func welcome (){
  print ("Welcome!")
}
```

## Class Structure
- The order of content in classes, structures and the like:
  1. Private static properties
  2. Public static properties
  3. Private properties
  4. Public properties
  5. Initializers
  6. Subclass overrides
  7. Public methods
  8. Private methods
- Extensions on a custom type should generally be defined in the same source file below the definition of the type itself.
- Extensions on Apple's types should be placed in their own file, typically inside of an "Extensions" folder in your project.
- Protocols should be added to a separate file with the protocol name in the same folder as the class.
- No vertical indents at the beginning and at the end (look at the Example class in the example).

🥰
```swift
class Example: ExampleProtocol {
    private static let privateStaticProperty = // something
    static let publicStaticProperty = // something

    private let privateProperty = // something
    let publicProperty = // something

    init () {
        // something
    }
    
    init (with parameter: Type) {
        // something
    }

    override func overrideFunction () {
        super.someFunc()
        // something
    }

    func publicMethod () {
        // something
    }

    private func privateMethod () {
        // something
    }
}

extension Example: ExampleProtocol {
    // something
}
```
🤮
```swift
class Example: ExampleProtocol {

    private static let privateStaticProperty = // something
    
    static let publicStaticProperty = // something
    
    private func privateMethod () {
        // something
    }

    private let privateProperty = // something

    init () {
        // something
    }
    override func overrideFunction () {
        super.someFunc()
        // something
    }
    
    init (with parameter: Type) {
        // something
    }

    func publicMethod () {
        // something
    }
    
    let publicProperty = // something
    
}
```

## Protocols
- When a class conforms to several protocols, they need to be split into different extensions. This approach will help group related methods together with the protocol they will conform. The protocol must also be marked with // MARK: -.
- In the name of the protocols, the word "Protocol" is allowed only at the end.

🥰
```swift
class ExampleConstroller: UIViewController {
    // something
}


// MARK: - UITableViewDataSource
extension ExampleConstroller: UITableViewDataSource {
    // something
}


// MARK: - UIScrollViewDelegate
extension ExampleConstroller: UIScrollViewDelegate {
    // something
}
```
🤮
```swift
class ExampleConstroller: UIViewController, UITableViewDataSource, UIScrollViewDelegate {
    // something
}
```

## Types
- If possible, you should use native Swift types (Double, String, Date), and not the old types from Objective-C (NSNumber, NSString, NSDate).
- Swift has transformations that turn Swift types into legacy Objective-C types. Therefore, when you need some old type, you can always get it from the Swift.

🥰
```swift
let number = 88.0                                     // Double
let stringNumber = (number as NSNumber).stringValue   // String
```
🤮
```swift
let number: NSNumber = 88.0                          // NSNumber
let stringNumber: NSString = number.stringValue       // NSString
```

## Forced Unwrapping
- Forced unwrapping of optionals is not permitted. Instead, proper error handling should be employed through the use of a safe unwrapping mechanism like guard, if let, optional chaining, or nil-coalescing.

🥰
```swift
var exampleOptional: String?

guard let text = exampleOptional else { return }
exampleVariable = text
```
```swift
var exampleOptional: String?

if let text = exampleOptional {
    exampleVariable = text
}
```
```swift
var exampleOptional: String?

exampleVariable = exampleOptional ?? "default value"
```
```swift
exampleClosure { [weak self] response in
guard let self = self { return }
// something
```
🤮
```swift
var exampleOptional: String?

exampleVariable = exampleOptional!
```
```swift
var exampleOptional: String?

if exampleOptional != nil {
    exampleVariable = exampleOptional!
}
```
```swift
exampleClosure { [weak self] response in
self?.exampleMethod()
```

## Forced Casting
- For the same reasons outlined above regarding forced unwrapping, forced casting is not permitted.

🥰
```swift
func exampleParse (from dictionary: [Int: Any]) {
    guard let euro = dictionary["euro"] as? Int,
          let usd = dictionary["usd"] as? Int else { return }
    // something
}
```
🤮
```swift
func exampleParse (from dictionary: [Int: Any]) {
    let euro = dictionary["euro"] as! Int
    let usd = dictionary["usd"] as! Int
    // something
}
```

## Enum Cases
- Enum cases should be declared on separate lines instead of declaring multiple cases on a single line.

🥰
```swift
enum ExampleEnum {
    case caseOne
    case caseTwo
    case caseThree
}
```
🤮
```swift
enum ExampleEnum {
    case caseOne, caseTwo, caseThree
}
```

## Spacing
- It's very simple: either one line (but not more) or not.
- And what in which case, see below.

### Inter-function
> One line

🥰
```swift
func up () {  
    // something
}

func down () {
    // something
}
```
🤮
```swift
func up () {  
    // something
}
func down () {
    // something
}
```

### For Extension, Protocols, Classes, etc.
> There must be no space after the opening declaration of the extension and at the end.

🥰
```swift
extension Example {
    func up () {
        // something
    }

    func down () {
        // something
    }
}
```
🤮
```swift
extension Example {

    func up () {
        // something
    }

    func down () {
        // something
    }
    
}
```

## Magic Numbers
- Don't store constants in an incomprehensible number format.
- Use component display.

🥰
```swift
let seconds = 60 * 60 * 60
```
🤮
```swift
let seconds = 3600
```

## Comments
- Add a dash after the MARK: so that Xcode's method browser will include nice visual separators.
- Only titles are allowed, not description or solid text.
- It is advisable to put an empty line after.
- After a double slash, 1 space is required.

🥰
```swift
// MARK: - Example Parse

func exampleParse (from dictionary: [Int: Any]) {
    guard let euro = dictionary["euro"] as? Int,
          let usd = dictionary["usd"] as? Int else { return }
    // something
}
```
🤮
```swift
//MARK: Stupid, unnecessary description, don't understand why.
func exampleParse (from dictionary: [Int: Any]) {
    guard let euro = dictionary["euro"] as? Int,
          let usd = dictionary["usd"] as? Int else { return }
    // something
}
```

[Go To Top](#skobelkins-code-style)
