---
title: rmx docs - scripts
---

# scripts

Scripts are blocks of code which control the behavior or effects of units,
spells, auras etc. Scripts are written in [Coffee-Script][coffee-script], and
run in a sandboxed context with only limited access to the game state.

## Script Environment

Here is a list of all functions available in the script environment.

### self

Self refers to the object which the script is controlling (behavior scripts),
the object which is casting the spell (spell scripts) or the object which has
the aura (aura scripts).

### scheduleEvent(...)

See ...


[coffee-script]: http://coffeescript.org/
