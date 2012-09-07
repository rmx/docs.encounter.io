---
title: rmx docs - unit
---

# Unit

Units are world objects which can be controlled by players or behavior
scripts. They also have a model and appearance so they are displayed on the
client in the canvas.

The WorldObject is the base object in the hierarchy. It contains the most
basic properties which are inherited by all other object types.



### isAlive :: Boolean

True if the unit is alive, can move, cast and otherwise interact with the
world.


### declareDead :: undefined

Declaring a unit dead will interrupt the current spellcast, remove all auras,
make the unit immovable and inform all players that this unit died.


## Attributes

Attributes are key/value pairs attached to a unit. There are a few basic
attributes, and you can also create your own.

 - `health`: When this attribute reaches zero then the unit has died. This is
   displayed in the client UI as the health bar. The game engine will clamp
   this value between zero and `max-health`.
 - `max-health`: The maximum health that the unit can have.
 - `speed`: The speed controls how fast the unit can walk. The default speed
   is 1.0, when set to zero then the unit may not move (but can still cast).


### setAttribute(name, value) :: undefined

It is recomended to use numeric values. It will allow you to use functions
like `changeAttributeBy`.

### getAttribute(name) :: polymorphic

The function either returns the attribute or undefined if the attribute is not
set.

### changeAttributeBy(name, delta) :: undefined

Change the attribute by the given delta. This only works if the value exists
and is numeric.


## Spells and Cooldowns

A unit can cast only one spell at a time. Casting a spell may take some time,
during that time the unit may or may not move. Spells can be interrupted. Each
spell is part of a cooldown group, all spells in that group share the same
cooldown. Once a spell is successfully cast, no spell in the same cooldown
group may be cast until the cooldown expires.


### startCast(name, target) :: Boolean

Start casting a spell. Returns true if the cast was started, and false if not
(because unit is incapable of casting, or another spell is being cast etc).

### interruptCurrentSpell() :: Boolean

Interrupt the current spell. Returns true if the spell was interrupted, false
otherwise (also when no spell is currently being cast).

### isCasting() :: Boolean

Returns true if a spell cast is in progress.

### triggerCooldown(group, time) :: undefined

The cooldown for the spell's cooldown group is automatically triggered after
a successful spell cast. But you can also manually trigger cooldowns for
other groups at any time.

### isCooldownExpired(group) :: Boolean

Returns true if the cooldown for that group has expired.


## Aura

Each unit has a list of auras. The auras can strengthen or weaken the unit by
accessing and modifying the combat log events during each tick.

**TODO**: Document how/when auras are triggered, refreshed etc.

### addAura(name) :: undefined

### hasAura(name) :: Boolean

### triggerAura(name) :: undefined

### removeAura(name) :: undefined

### clearAuras :: undefined

Remove all auras from the unit. Is the same as calling `removeAura` for each
aura that is currently on the unit.
