---
title: rmx docs - scripts
---

# Scripts

Scripts are blocks of code which control the behavior and effects of units,
spells, auras etc. Scripts are written in [Coffee-Script][coffee-script], and
run in a sandboxed context with only limited access to the game state.


## Script Context

The script context exposes accessors to the game state and useful helper
functions. Here is a list of all symbols available in the script environment.


### self :: WorldObject

Self refers to the object which the script is controlling (behavior scripts),
the object which is casting the spell (spell scripts) or the object which has
the aura (aura scripts).


### scheduleEvent(delay, target, func, args...) :: undefined

Use this function to schedule an event after a certain delay. The delay is
a positive number of miliseconds after which to apply the event. The function
can be any of the publicly available functions on the target object.

This example adds the `Renew` aura to the caster after three seconds:

    scheduleEvent 3000, self, 'addAura', 'Renew'

Not all functions make sense to schedule in an event. As an example: While the
system happily accepts an event which calls `getAttribute`, it will not
actually have any effect on the game state, as the function merely queries the
attribute.

Calling an undefined function will cause a fatal error which immediately
aborts the game.


### worldObjects :: Array

The array of all objects in the world. You can use the `filter` function to
filter these objects to select only those that you want. The following example
gets a list of objects within 5 meters of self:

    targets = worldObjects.filter (obj) ->
        self.distanceToObject(obj) < 5


[coffee-script]: http://coffeescript.org/
