---
title: API - WorldObject
---

# WorldObject

A WorldObject is an object which is located at a certain position within
a terrain. It has a model which is rendered on the client.


## Position

Each WorldObject has a position in the world. You can query the position and
move the object somewhere else.



## Phase

Each object exists in a certain phase. A phase is identified by a string. Only
objects within the same phase can see each other. The default phase is `null`.



## Attributes

Attributes are key/value pairs attached to a WorldObject. There are a few
basic attributes, and you can also create your own.

 - `health`: When this attribute reaches zero then the WorldObject has died.
   This is displayed in the client UI as the health bar. The game engine will
   clamp this value between zero and `max-health`.
 - `max-health`: The maximum health that the unit can have.



## Spells and Cooldowns

A WorldObject can cast only one spell at a time. Casting a spell may take some
time, during that time the object may or may not move. Spells can be
interrupted. Each spell is part of a cooldown group, all spells in that group
share the same cooldown. Once a spell is successfully cast, no spell in the
same cooldown group may be cast until the cooldown expires.



## Aura

Each WorldObject has a list of auras. The auras can strengthen or weaken the
unit by accessing and modifying the combat log events during each tick.
