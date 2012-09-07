---
title: rmx docs - scripts - spell
---

# Spell

Spells are actions which a unit can perform. A spell is cast on a target. This
can be a `WorldObject` or a position on the terrain. A spell also has a cast
time. That is the time during which the unit must stand still to fully
concentrate on the spell casting. Performing any other action, or even simply
moving, will cancel the spellcast.


### cast(WorldObject) :: undefined

This function is called when the spell cast successfully executed. The first
argument is the WorldObject target on which the spell was cast.
