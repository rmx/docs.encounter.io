---
title: API - Terrain
---

# Terrain


## Movement and Terrain Positions

All `WorldObjects` are located at a `TerrainPosition`. Computing

### getTerrainPosition(tile, local_x, local_y) :: TerrainPosition

Return the "global" terrain position corresponding to `(local_x, local_y)` in
the specified tile.


### moveTowards(guid, velocity = 1.0, min_distance = 0.0) :: undefined

Convenient method for creatures to walk towards a player or position. TODO.
