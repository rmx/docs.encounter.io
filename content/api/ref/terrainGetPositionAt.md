---
title: API - Reference - terrainGetPositionAt
---

### terrainGetPositionAt :: (String, Number, Number, Number) -> TerrainPosition

Create a `TerrainPosition` which represents the position at the x/y/z
coordinates within the terrain instance identified by the tag. The `z`
component does not need to be accurate. The function will project the position
to the closests surface.


## Example

```coffeescript
pos = terrianGetPositionAt 'default', 0.3, 0.7, 0.5
```


## See Also

[terrainCreate](/api/ref/terrainCreate/)
