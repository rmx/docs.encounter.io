---
title: API - Reference - unitWalkTo
---

### unitWalkTo :: (WorldObject, TerrainPosition) -> Boolean

Uses the pathfinder to first compute a path from the units position to the
specified end position and then starts walking. Returns true if a path could
be computed. Consecutive calls to this method overwrite previous move
commands.
