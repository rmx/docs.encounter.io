---
title: API
---

# Overview

The scripts you write run in a sandboxed context and where they have access to
the following symbols and functions.


### currentTime :: Number

The in-game time is represented by a number, counting the seconds since an
arbitrary point in the past. For example, you can save the current time in the
constructor and then calculate how long it has been when a certain events
occurs.

    constructor: ->
        @createdAt = currentTime

    filterEvent: (e) ->
        diff = currentTime - @createdAt


### self :: WorldObject

Self refers to the object which the script is controlling (behavior scripts),
the object which is casting the spell (spell scripts) or the object which has
the aura (aura scripts).


### worldObjects :: [ WorldObject ]

The list of all objects in the world. You can use the `listFilter` function to
filter these objects to select only those that you want. The following example
gets a list of objects within 5 meters of self:

    targets = listFilter worldObjects, (obj) ->
        distanceBetween(self, obj) < 5

### players :: [ Player ]

All players which are participating in the game.



## Events

Scripts can not directly change the game state. They must use events to do so.
This allows other scripts to react to these events. How to create events is
described in later sections. Once you have an event you have to either
schedule it to be executed at some point in the future, or append it to
another event.


### eventSchedule :: (Number, Event) -> undefined

Use this function to schedule an event after a certain delay. The delay is
a positive number of seconds after which to apply the event.

This example adds the `Renew` aura to the caster after three seconds:

    event = unitAddAura self, 'Renew'
    eventSchedule 3, event


### eventAppend :: (Event, Event) -> undefined

Append an event as a reaction to another event. The first argument is the
event to which you want to append the reaction. You would usually use this in
the `filterEvent` function to react to certain events.

This example heals `self` when any event occurs within the game.

    filterEvent: (e) ->
        reaction = unitChangeAttributeBy self, 'health', +10
        eventAppend e, reaction


### eventName :: (Event) -> String

Extract the event name. You find the event names [here](/events/misc/) and on
other related pages.

### eventArg :: (Event, Number) -> Any

Get the event argument at the given index.


### eventData :: (Event, String) -> Any

Get the named event property from the event. Throws an exception if the
property does not exist in the given event. You should check with `eventName`
first to see if you're dealing with the correct event.

    if (eventName e) == 'finishGame' && (eventData e, 'outcome') == 'victory'
            # The game has finished and players have won.


## Parameters

Parameters are values which you can access in your scripts. You use them to
parametrize the effects of your spells or auras. For example, instead of
hardcoding the damage or heal in your scripts, you'd use parameters. This
allows you to fine-tune your encounter without having to create a new version
of your spell or aura every time you need to adjust its effects.


### paramGet :: (Function, String) -> Any

Get a parameter by its name. The first argument is a function which will
convert the string into any type you want. You can use the predefined
functions `Number` or `String` to convert the parameter to a Number or String,
respectively. If the conversion function returns undefined, the game will
throw an exception.

    damage = paramGet Number, 'BaseSpellDamage'
