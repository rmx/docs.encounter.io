---
title: rmx docs - world object
---

# WorldObject

The WorldObject is the base object in the hierarchy. It contains the most
basic properties which are inherited by all other object types.


## Position

Each WorldObject has a position in the world. You can query the position and
move the object somewhere else.


### getPosition :: Position

The position is represented by a special object. It stores the tile in which
the object is, and the position within the tile.


### getWorldPosition :: Vector3

The world position is a three-element array, containing the x/y/z coordinates
of the object.


### teleport(Position) :: undefined

Teleport the object to the given position.


### distanceToObject(WorldObject) :: Number

Return the euclidean distance between this and the other object.
