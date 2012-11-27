---
title: API - Reference - unitAttributeGet
---

### unitAttributeGet :: (WorldObject, String) -> Number

Get the attribute. The example below sets the health to 50% of its current
value.


## Examples

```coffescript
currentHealth = unitAttributeGet self, 'health'
event         = unitAttributeSet self, 'health', currentHealth * 0.5
eventSchedule 0, event
```
