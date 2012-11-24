---
title: API - Objectives
---

# Objectives

Objectives are hints that are displayed on the client, They show the player
what he has to complete in order to win the game. They are optional, it's
perfectly ok to not show any objectives and let the player figure out himself
what to do.

Currently only WorldObjects can be objectives. If a WorldObject is marked as
objective (the _boss_ which has to be killed), its health bar is dislpayed in
the objective list on the client (top right corner). This way the _boss_ is
always visible to all players, even if the player doesn't have the boss in its
target (useful for _healer_ roles, which usually have one of their team
members targetted).

Newly created objectives are marked as _not cleared_. Meaning they have not
yet been completed. Once the objective is completed, you can mark it as
_cleared_. The client will display cleared objectives with a green-ish color.

Once an objective is cleared, it can not be un-cleared again. But you can
remove objectives, if you want to guide the players through multiple
consecutive objectives.


### createObjective :: (WorldObject) -> undefined

Create a new objective from the given WorldObject.


### clearObjective :: (WorldObject) -> undefined

If the given WorldObject is an objective, mark it as cleared.


### removeObjective :: (WorldObject) -> undefined

If the given WorldObject is an objective, remove it.
