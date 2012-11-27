---
title: API - Reference - unitTriggerCooldown
---

### unitTriggerCooldown :: (WorldObject, String, Number) -> Event

Trigger a cooldown. A cooldown will prevent the object from casting spells in
that cooldown category for the given amount of time. Many spells are in the
`GLOBAL` cooldown category. This category usually has a short cooldown (1.5
seconds) and is used to prevent the player from casting spells rapidly after
each other.


## Examples

```coffeescript
event = unitTriggerCooldown self, 'GLOBAL', 1.5
eventSchedule 0, event
```
