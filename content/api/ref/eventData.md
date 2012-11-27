---
title: API - Reference - eventData
---

### eventData :: (Event, String) -> Any

Get the named event property from the event. Throws an exception if the
property does not exist in the given event. You should check with `eventName`
first to see if you're dealing with the correct event.


## Example

```coffeescript
if (eventName e) == 'finishGame' && (eventData e, 'outcome') == 'victory'
        # The game has finished and players have won.
```


## See Also

[eventArg](/api/ref/eventArg/),
[eventName](/api/ref/eventName/)
