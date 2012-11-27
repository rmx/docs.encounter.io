---
title: API - Reference - eventSchedule
---

### eventSchedule :: (Number, Event) -> undefined

Use this function to schedule an event after a certain delay. The delay is
a positive number of seconds after which to execute the event.


## Examples

```coffeescript
event = unitAddAura self, 'Renew'
eventSchedule 3, event
```

## See Also

[eventAppend](/api/ref/eventAppend/)
