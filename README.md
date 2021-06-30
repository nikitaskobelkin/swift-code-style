# Skobelkin's code style

My principles of coding style in my projects for me and my friends.

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
