---
title: API - Reference - currentTime
---

### currentTime :: Number

The current time in the game. It's represented as the number of seconds since
an unspecified time in the past.


## Examples

```coffeescript
class Aura

    constructor: ->
        @startedAt = currentTime

    handleEvent: ->
        diff = currentTime - @startedAt
```

## See Also

[eventSchedule](/api/ref/eventSchedule/)
