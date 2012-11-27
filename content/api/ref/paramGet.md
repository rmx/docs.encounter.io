---
title: API - Reference - paramGet
---

### paramGet :: (Function, String) -> Any

Get a parameter by its name. The first argument is a function which will
convert the string into any type you want. You can use the predefined
functions `Number` or `String` to convert the parameter to a Number or String,
respectively. If the conversion function returns undefined, the game will
throw an exception.


## Example

```coffeescript
damage = paramGet Number, 'BaseSpellDamage'
```
