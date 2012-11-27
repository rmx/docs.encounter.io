---
title: API - Reference - unitAttributeChangeBy
---

### unitAttributeChangeBy :: (WorldObject, String, Number) -> Event

Change the named attribute by the given delta. If the attribute does not
exist, or is not a Number, then the game will throw an exception.


## Examples

```coffescript
event = unitAttributeChangeBy self, 'health', +10
eventSchedule 5, event
```
