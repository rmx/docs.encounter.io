---
title: API - Reference - worldGetUnits
---

### worldGetUnits :: () -> [ WorldObject ]

The list of all objects in the world. You can use the `listFilter` function to
filter these objects to select only those that you want. The following example
gets a list of objects within 5 meters of self:

    targets = listFilter worldGetUnits(), (obj) ->
        distanceBetween(self, obj) < 5
