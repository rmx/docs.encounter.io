---
title: API - Terrain
---

# Terrain

## Types

### TerrainPosition

Describes a position within a terrain. Each WorldObject has such a position.
You can create new positions from a terrain and a position within the terrain
(`terrainGetPositionAt`), or get from a WorldObject using `unitGetPosition`.


## Functions


### terrainCreate :: (String, String) -> undefined

Create a new instance of a terrain. Each instance is identified by a unique
tag. You can use this tag to refer to the instance. If your encounter has only
one terrain, the convention is to use the `'default'` tag. You should create
at least one terrain instance in the Glue constructor. Later during the game
you can create additional instances if required.

The tag must be unique. If your encounter uses multiple terrain instances,
it's up to you to make sure that the tags are unique. If you try to use a tag
which already exists, the game will throw an exception.


    class Glue
        constructor: ->
            terrainCreate 'Maze', 'default'


### terrainGetPositionAt :: (String, Number, Number, Number) -> TerrainPosition

Create a `TerrainPosition` which represents the position at the x/y/z
coordinates within the terrain instance identified by the tag. The `z`
component does not need to be accurate. The function will project the position
to the closests surface.

    pos = terrianGetPositionAt 'default', 0, 0, 0


### terrainGetTileByIndex :: (String, Number) -> TerrainTile

### terrainPositionGetTile :: (TerrainPosition) -> TerrainTile

### terrainPositionSetFacing :: (TerrainPosition, Number) ->

### terrainTileGetPosition :: (TerrainTile, Number, Number) -> TerrainPosition
