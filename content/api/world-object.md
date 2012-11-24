---
title: API - WorldObject
---

# WorldObject

A WorldObject is an object which is located at a certain position within
a terrain. Each WorldObject has a (non-unique) name, and a model associated
which is used to render the object on the client.


## Types

### WorldObject

You can create new world objects using `worldCreateUnit`, and can list all
world objects using `worldGetUnits`.


## Functions

### worldCreateUnit :: (String, String, String, TerrainPosition) -> WorldObject

Create a new `WorldObject`. The name does not need to be unique.

    worldCreateUnit role, name, behavior, pos


### worldDeleteUnit :: (WorldObject) -> undefined

Remove the given WorldObject from the game. This causes the object to be
immediately disappear on the client.



## Position

Each WorldObject has a position in the world. You can query the position and
move the object somewhere else.


### unitGetPosition :: (WorldObject) -> TerrainPosition

Return the position at which the given object is located. The position is
always valid.


### unitTeleportTo :: (WorldObject, TerrainPosition) -> Event

Teleport the WorldObject to a new position. The only constraints are that the
new position must be valid. No speed, line in sight checks etc are performed.
The new position may even be in a completely new terrain.



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


### unitAttributeGet :: (WorldObject, String) -> Number

Get the attribute. The example below sets the health to 50% of its current
value.

    currentHealth = unitAttributeGet self, 'health'
    event         = unitAttributeSet self, 'health', currentHealth * 0.5
    eventSchedule 0, event


### unitAttributeChangeBy :: (WorldObject, String, Number) -> Event

Change the named attribute by the given delta. If the attribute does not
exist, or is not a Number, then the game will throw an exception.

    event = unitAttributeChangeBy self, 'health', +10
    eventSchedule 5, event


### unitAttributeSet :: (WorldObject, String, Number) -> Event

Set an attribute. Currently we restrict the values to Numbers.


## Spells and Cooldowns

A WorldObject can cast only one spell at a time. Casting a spell may take some
time, during that time the object may or may not move. Spells can be
interrupted. Each spell is part of a cooldown group, all spells in that group
share the same cooldown. Once a spell is successfully cast, no spell in the
same cooldown group may be cast until the cooldown expires.


### unitStartCast :: (WorldObject, String, WorldObject) -> Event

Start casting a spell on a target. The target is always a WorldObject.
Currently it's not possible to start casting a spell on an arbitrary position.


### unitInterruptCast :: (WorldObject) -> Event

Interrupt the spellcast. If the object is not casting any spell, the event has
no effect.


### unitTriggerCooldown :: (WorldObject, String, Number) -> Event

Trigger a cooldown. A cooldown will prevent the object from casting spells in
that cooldown category for the given amount of time. Many spells are in the
`GLOBAL` cooldown category. This category usually has a short cooldown (1.5
seconds) and is used to prevent the player from casting spells rapidly after
each other.

    event = unitTriggerCooldown self, 'GLOBAL', 1.5
    eventAppend e, event

## Aura

Each WorldObject has a list of auras. The auras can strengthen or weaken the
unit by accessing and modifying the combat log events during each tick.


### unitAuraAdd :: (WorldObject, String) -> Event

### unitAuraRemove :: (WorldObject, String) -> Event

### unitAuraTrigger :: (WorldObject, String) -> Event

### unitAuraIsPresent :: (WorldObject, String) -> Boolean

Return true if the object has an aura active with the given name.


## Movement generator

### unitWalkTo :: (WorldObject, TerrainPosition) -> Boolean

Uses the pathfinder to first compute a path from the units position to the
specified end position and then starts walking. Returns true if a path could
be computed. Consecutive calls to this method overwrite previous move
commands.


### unitMoveAlongPath :: (WorldObject, [ TerrainPosition ]) ->

Moves a unit along a list of terrain positions (waypoints). Consecutive calls
to this method overwrite previous move commands
