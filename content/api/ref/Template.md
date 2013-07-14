---
title: API - Reference - Template
---

### type Template


## Required properties

 - `attributes :: List[ { name :: String, value :: Number } ]`
 - `health :: Number`
 - `model :: String`
 - `position :: TerrainPosition`
 - `spells :: List[String]`


## Optional properties

 - `behavior :: String`
 - `faction :: String`
 - `maxHealth :: Number`
 - `movementSpeed :: Number`
 - `scale :: Number`


## Example

```language-coffeescript
baseTemplate = worldObjectTemplate "Monster"
bossMirrorTemplate = bossTemplate { movementSpeed: 1 }

position = terrainGetPositionAt "terrain", 0, 0, 0
createWorldObject bossMirrorTemplate { position }
```


## See Also

[worldObjectTemplate](/api/ref/worldObjectTemplate/),
[createWorldObject](/api/ref/createWorldObject/)
