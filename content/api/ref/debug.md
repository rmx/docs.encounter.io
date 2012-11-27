---
title: API - Reference - debug
---

### debug :: (String) -> undefined

In test games, this sends the given string to all clients where it is
displayed in the console. This allows you to trace your scripts and see what
they are doing. It is safe to leave the debug statements in your scripts when
you release your revision, ordinary players will not see the debug messages.
However, keep in mind that too many debug statements may slow down the client.


## Example

```coffeescript
handleEvent: (e) ->
    debug "Got event: " + (eventName e)
```
