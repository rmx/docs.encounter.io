---
title: API - Achievements
---

# API: Achievements

Achievements are awards that a player receives for outstanding performance.
They are unique per encounter, meaning that a player can collect the same
achievement twice if he plays two different encounters which feature the same
achievement.

All collected achievements are displayed on the players' publc profile page.
If the player has collected the same achievement in multiple encounters, we
display something along this:

Achievement _Speed Run_, awarded in 42 encounters.


### awardAchievement :: (Player, Achievement) -> undefined

Award an achievement to a player.


### controllingPlayer :: (WorldObject) -> Maybe Player

If the given WorldObject is controlled by a player, then return the player.
Otherwise return null.
