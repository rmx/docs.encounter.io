---
title: Game Mechanics
---

These are the builtin game mechanics that are valid for all games. Scripts can
not influence these. Players and designers can rely on these properties.


## Players

 - A game is played by one or more players.
 - Players are grouped into teams (currently only a single team is possible).
 - Each player controls exactly one WorldObject.


## Primary attribute

 - The primary attribute of each WorldObject is `health`.
 - If the attribute is zero at the end of a tick, the object is declared dead.
 - This attribute is displayed in the client UI at all times.


## Spellcasting

 - A WorldObject can cast only one spell at any given time.
 - Any requests to start a spellcast are silently ignored if:
    - The caster is dead.
    - The caster is already casting a spell.
