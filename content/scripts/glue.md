---
title: Scripts - Glue
---

# Glue

The Glue script is where you initialize the whole encounter. The class is
instanciated just after the server has initialized the game. You should create
all necessary terrains and world objects in the constructor.


### getSpawnLocation(role) :: TerrainPosition

This function is called once for each player that is participating in the
game. It must return the `TerrainPosition` at which the player should be
put, e.g.,

    getSpawnLocation: (role) ->
        return getTerrainPosition 'default', 0, 0.5, 0.5

meaning all players (regardless of role) will spawn in tile `0` at local
coordinates `(0.5, 0.5)`.
