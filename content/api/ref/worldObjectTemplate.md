---
title: API - Reference - worldObjectTemplate
---

### worldObjectTemplate :: (String) -> Template

Retrieve a template (role) from the database. The `Template` can be passed to
`createWorldObject` to instanciate a `WorldObject`. The Template is also
a function which can be called to refine or update the template, eg.

    baseTemplate = worldObjectTemplate "Monster"
    bossMirrorTemplate = bossTemplate { movementSpeed: 1 }

the recognized properties are described in [Template][/api/ref/Template/].
