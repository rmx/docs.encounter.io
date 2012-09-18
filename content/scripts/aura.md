---
title: encounter docs - scripts - aura
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



## Aura Options

An optional option dictionary can be passed to the `addAura` event to propagate
information of auras across units.

    options = { numberOfCharges: 10, stacks: 5, duration: 5 }
    target.addAura 'aura name', options

Some of the option names are reserved for displaying aura information in the
UI:

* `stacks`: number of aura stacks
* `duration`: remaining duration the aura is active

Note: The `duration` field will be used as a default duration of an aura and a
`removeAura` event will be scheduled automatically on `start`.


## Convenience Functions

To facilitate aura handling we provide the following convenience functions:

### changeAuraDuration(target, name, delta_t) :: undefined

Increases or decreases the aura (`name`) duration on `target` by `delta_t`.
Pending `removeAura` events are altered when this function is invoked.


