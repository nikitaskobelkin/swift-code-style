# Skobelkin's code style

My principles of coding style in my projects for me and my friends.

1. [General](#general)
2. [Naming](#naming)

## General
- Global constants are not allowed, they must always be inside the namespace.
- Compiler warnings are considered bugs and are not allowed. Exception: TODO :, FIXME:
- Follow the typing rules (even in comments).

**Do**
```
// A comment that someone left (for example, I), here we will put an end.
```
**Do Not**
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

**Do**
```swift
class Weather {
  var cityName: String
  var cloudy: String
}
```
**Do Not**
```swift
class weather {
  var City_NAME: String
  var cldly: String
}
```
