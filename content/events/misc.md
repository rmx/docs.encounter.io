---
title: Events - Miscellaneous
---

# Miscellaneous

### startGame :: { }

The players have started the game. For example by engaging the enemy. Calling
`gameDidStart` will cause this event to be fired.


### finshGame :: { outcome :: String }

The game has ended. The outcome property indicates whether the players have
won (`victory`) or lost (`defeat`) the game. Calling `gameDidEnd` will cause
this event to be fired.


### moveTo :: (WorldObject, Position)

A WorldObject has moved. The event includes the new position where the object
is located now.


### speak :: (WorldObject, String)

A WorldObject has spoken. Chat does not count as speaking (though maybe it
should).
