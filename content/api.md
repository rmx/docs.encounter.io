---
title: API
---

# Overview

The scripts you write run in a sandboxed context and where they have access to
the following symbols and functions.



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


## Parameters

Parameters are values which you can access in your scripts. You use them to
parametrize the effects of your spells or auras. For example, instead of
hardcoding the damage or heal in your scripts, you'd use parameters. This
allows you to fine-tune your encounter without having to create a new version
of your spell or aura every time you need to adjust its effects.
