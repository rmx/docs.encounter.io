---
title: rmx docs - scripts - aura
---

# Aura

Auras are attached to a WorldObject. They remain attached until they are
removed. An aura can also be triggered, either by itself or by another script.
And it can filter events: drop events altogether, modify event arguments or
attach reactions to the events.

Auras on a unit are unique by name. If you add an aura which already exists
on the unit, it is up to your script what should happen.

These are the functions which are used by the game engine. All functions are
optional.


### start :: undefined

Called just after the aura is first attached to a unit. This function is called
exactly onece.


### refresh :: undefined

When the aura is already attached to the unit, `addAura` calls this function.
You can chose whether to reset the state, ignore the event, or to stack the
aura (eg. multiple stacks increase the effect).


### trigger :: undefined

The `triggerAura` event directly calls this function. The use-case here is to
trigger your aura whenever it should do something. If your trigger function
triggers itself, this can also be used to implement periodic actions.


### remove :: undefined

Called by the `removeAura` event.


### hasFinished :: Boolean
