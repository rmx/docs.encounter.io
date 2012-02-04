---
title: rmx docs - world object
---

# WorldObject

The WorldObject is the base object in the hierarchy. It contains the most
basic properties which are inherited by all other object types.


## Position

Each WorldObject has a position in the world. The position is a x/y/z tuple.


### getPosition :: Array

The position is a three-element array, containing the x/y/z coordinates.


### moveToPosition(x, y, z) :: undefined

Moving an object dispatches an Event.
