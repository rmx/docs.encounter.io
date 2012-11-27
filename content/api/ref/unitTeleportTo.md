---
title: API - Reference - unitTeleportTo
---

### unitTeleportTo :: (WorldObject, TerrainPosition) -> Event

Teleport the WorldObject to a new position. The only constraints are that the
new position must be valid. No speed, line in sight checks etc are performed.
The new position may even be in a completely new terrain.
