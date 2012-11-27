---
title: API - Reference - eventAppend
---

### eventAppend :: (Event, Event) -> undefined

Append an event as a reaction to another event. The first argument is the
event to which you want to append the reaction. You would usually use this in
the `filterEvent` function to react to certain events.


## Examples

```coffeescript
filterEvent: (e) ->
    reaction = unitChangeAttributeBy self, 'health', +10
    eventAppend e, reaction
```

## See Also

[eventSchedule](/api/ref/eventSchedule/)
