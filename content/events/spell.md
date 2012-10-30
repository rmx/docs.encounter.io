---
title: Events - Spell
---

# Spell

### attemptSpellcast :: (WorldObject, Spell, SpellTarget)

Emitted when the world object is about to attempt to cast a spell. It is
followed by either `failSpellcast` or `startSpellcast`.


### failSpellcast :: (WorldObject, Spell, SpellTarget)

The caster attempted to cast a spell, but it failed because the preconditions
were not met (target is out of range, cooldown has not cleared yet etc).


### startSpellcast :: (WorldObject, Spell, SpellTarget)

The caster has started casting a spell.


### finishSpellcast :: (WorldObject)

The caster has finished casting its spell.


### cancelSpellcast :: (WorldObject)

The caster has canceled the cast.


### interruptSpellcast :: (WorldObject)

The caster was interrupted while casting his spell.
