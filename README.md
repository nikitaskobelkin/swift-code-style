# Skobelkin's code style

My principles of coding style in my projects for me and my friends.

1. [General](#general)
2. [Naming](#naming)
3. [Structure](#structure)
4. [Class (Struct) structure](#class-structure)

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

### For variables and functions
> Beginning with lowercase.

### For classes, structures, enums, etc.
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

## Class structure
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
