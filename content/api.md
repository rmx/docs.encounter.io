---
title: API
---

## Events

Scripts can not directly change the game state. They must use events to do so.
This allows other scripts to react to these events. How to create events is
described in later sections. Once you have an event you have to either
schedule it to be executed at some point in the future, or append it to
another event.


## Parameters

Parameters are values which you can access in your scripts. You use them to
parametrize the effects of your spells or auras. For example, instead of
hardcoding the damage or heal in your scripts, you'd use parameters. This
allows you to fine-tune your encounter without having to create a new version
of your spell or aura every time you need to adjust its effects.
