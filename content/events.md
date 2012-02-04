---
title: rmx docs - events
---

# events

An event is a function name and arguments, which shall be called on a target
object at a certain point in the future. The event also includes information
about the origin and source objects. These are the objects which caused the
event to be generated.

You never directly create these events, but rather uses one of the many
wrappers that are available in a script context. This is to ensure that the
fields such as `source` and `origin` are properly set. It also makes it easier
because you don't have to worry about those.


### scheduleEvent(delay, target, func, args...)

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
