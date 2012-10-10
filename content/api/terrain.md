---
title: API - Terrain
---

## Movement and Terrain Positions

All `WorldObjects` are located at a `TerrainPosition`. Computing

### getTerrainPosition(tile, local_x, local_y) :: TerrainPosition

Return the "global" terrain position corresponding to `(local_x, local_y)` in
the specified tile.


### moveTowards(guid, velocity = 1.0, min_distance = 0.0) :: undefined

Convenient method for creatures to walk towards a player or position. TODO.


## Loading a Terrain and Spawn Locations

In order to load terrain and define spawn location the encounter glue file has
to implement the following two methods.

### loadTerrain(instance) :: undefined

E.g., after

    loadTerrain: (instance) ->
        instance.createTerrain "DrEvilsLair"

the terrain specified in 'DrEvilsLair.coffee' is loaded and upon bootstrapping
sent to all players.


### getSpawnLoaction(instance, player, role) :: undefined

Method sets spawn location of player or role, e.g.,

    getSpawnLocation: (instance, player, role) ->
        return instance.terrain.getTerrainPosition 0, 0.5, 0.5

meaning all players (regardless of role and player) will spawn in tile `0` at
local coordinates `(0.5, 0.5)`.
