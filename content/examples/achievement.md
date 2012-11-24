---
title: Example - Achievement
---

# Example: Achievement

This achievement, **Speed Run**, is awarded to players which complete the
encounter within a given time limit.

    # We store the time limit in a param, so we can easily tweak it.
    timeLimit = paramGet Number, 'speedRunLimit'

    # Helper which returns true if the event indicates that the game has
    # finished and players have won.
    isVictoryEvent = (e) ->
        (eventName e) == 'finishGame' && (eventData e, 'outcome') == 'victory'

    class Achievement

        constructor: ->
            @startedAt = null


        handleEvent: (e) ->

            # Store the time when players start the game (engage the boss).
            if (eventName e) == 'startGame'
                @startedAt = currentTime

            # If the players win the game within the limit, give them all this
            # achievement.
            else if (isVictoryEvent e) && currentTime - @startedAt < timeLimit
                forEach players, (x) -> awardAchievement x, self


    module.exports = Achievement
