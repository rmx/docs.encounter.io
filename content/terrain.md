---
title: encounter docs - terrain
---

# Terrain

The terrain class defines geometries of the worlds the players moves on. We
have the following conventions for tiles and models:

* `+z` is up
* `-x` is forward


A terrain is specified with two components. First we require one definition of a
"tile" for every tile present in the terrain. Subsequently these tiles can be
instantiated and positioned to represent worlds (best to use the in-browser
editor). Both components are specified in JSON as shown in the corresponding
sections.


## Tiles

Tiles are squares defining the origin of the local coordinate system in the
lower left front of the tile and has an extension to `[2, 2, 2]`. A tile has
size `[0, 2N^3)`.

![Tile specification](../assets/tile.png)

Tile IDs are unique names used for referencing by tile instances. The model name
corresponds to a OBJ model to be found in the `world` directory of the
encounter.

    tiles:
        tile_name:
            model          : "model_name"
            vertices       : [-1,-1,0, -1,1,0, 1,-1,0, 1,1,0]
            facesProject   : [0,1,2, 1,3,2]
            facesIntersect : []
            bbox           : {pmin:[-1,-1,-1], pmax:[1,1,1]}


### Creating Tiles with Blender

TODO.


## Tile Instances

Terrains are defined using the previously introduced tiles. Each tile instance
has a unique identifier and references the tile name it represents. Position and
rotation concertize the instance.

    data:
        0:
            tile: "tile_name",
            pos : [0,0,9],
            rot : 0

        1:
            tile: "tile_name",
            pos : [0,0,6],
            rot : 0

        2:
            tile: "another_tile",
            pos : [4,4,6],
            rot : 0


All rotations are anticlock-wise and the rotation axis is the origin of the
tile:

* 0: no rotation
* 1: rotated by 90 degrees
* 2: rotated by 180 degrees
* 3: rotated by 270 degrees



