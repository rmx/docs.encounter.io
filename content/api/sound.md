---
title: API - Sound
---

## Types

### SoundSettings

All time values are expressed in seconds.

 - duration :: Number
 - volume :: Number
 - delay :: Number
 - looped :: Boolean


## Function

### soundPlay :: (String, SoundSettings) -> ID

Start playing the sound. The settings specify the volume, delay etc. The
function returns the sound ID which you can use to stop the sound.

### soundStop :: (ID) ->

### terrainSetAmbientSound :: (String, String) ->
