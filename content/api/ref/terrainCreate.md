---
title: API - Reference - terrainCreate
---

### terrainCreate :: (String, String) -> undefined

Create a new instance of a terrain. Each instance is identified by a unique
tag. You can use this tag to refer to the instance. If your encounter has only
one terrain, the convention is to use the `'default'` tag. You should create
at least one terrain instance in the Glue constructor. Later during the game
you can create additional instances if required.

The tag must be unique. If your encounter uses multiple terrain instances,
it's up to you to make sure that the tags are unique. If you try to use a tag
which already exists, the game will throw an exception.


## Example

```coffeescript
class Glue

    constructor: ->
        terrainCreate 'Maze', 'default'
```


## See Also

[terrainGetPositionAt](/api/ref/terrainGetPositionAt/)
