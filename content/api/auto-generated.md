#  Global variables

 The scripts you write run in a sandboxed context and where they have access to the following symbols and functions.

### self 
> self  :: WorldObject

 Self refers to the object which the script is controlling (behavior scripts), 
 the object which is casting the spell (spell scripts) or the object which has the aura (aura scripts).



#  Events

 Scripts can not directly change the game state.
 They must use events to do so.
 This allows other scripts to react to these events.
 How to create events is described in later sections.
 Once you have an event you have to either schedule it to be executed at some point in the future, or append it to another event.

### eventSchedule 
> eventSchedule  :: (Number delay,  Event  event) -> undefined

 Use this function to schedule an event after a certain delay. The delay is a positive number of seconds after which to apply the event.

 This example adds the Renew aura to the caster after three seconds:

    event = unitAddAura self, 'Renew'
    eventSchedule 3, event


### eventAppend 
> eventAppend  :: (Event parent,  Event  child) -> undefined

 Append an event as a reaction to another event. The first argument is the event to which you want to append the reaction. You would usually use this in the filterEvent function to react to certain events.

 This example heals self when any event occurs within the game.

    filterEvent: (e) ->
        reaction = unitChangeAttributeBy self, 'health', +10
        eventAppend e, reaction



#  Game state



### gameDidStart 
> gameDidStart  :: ( ) -> undefined

 Starts the actual part of the game.
 Anything before this is considered the preparation phase.


### gameDidEnd 
> gameDidEnd  :: (Boolean victorious) -> undefined

 Ends the game.
 The argument defines whether the player(s) were successful or not.



#  PRNG

 Designers can access an [Alea](http://baagoe.org/en/w/index.php/Better_random_numbers_for_javascript)
 PRNG by using the following symbols in the script environment.

### random 
> random  :: ( ) -> Number

 Returns a random real number between 0 and 1


### random 
> random  :: (Number min,  Number  max) -> Number

 Returns a random real number in the given interval


### random 
> random  :: (Number min,  Number  max) -> Number

 Returns a random natural number in the given interval



#  Shuffle bag

 As discussed in many game designer communities (e.g. [Less-Random Generator](http://seanmonstar.com/post/708989796/a-less-random-generator)),
 a ?fair? less-random generator is preferable to avoid frustrating players,
 e.g., when having a 40% hit chance the player really expects to hit a creature twice out of five swings.
 This kind of controlled randomness can be implemented with a shuffle bag.
 A shuffle bag takes an arbitrary number of items, stuffs them into a bag and shuffles the items.
 When a random item is requested an item is drawn from the shuffle bag (and put aside).
 Once the bag is empty all items will be inserted (again) and the bag is shuffled (again).

### shuffleBagCreate 
> shuffleBagCreate  :: ( ) -> ShuffleBag

 Creates a new (empty) shuffle bag.


### shuffleBagAdd 
> shuffleBagAdd  :: (ShuffleBag bag,  Object  element) -> undefined

 Adds a new element to the shuffle bag
 Items can be added successively to a shuffle bag.
 The following example would add three items to the shuffle bag.

    shuffleBagAdd @shuffleBag, 'hit'
    shuffleBagAdd @shuffleBag, 'hit'
    shuffleBagAdd @shuffleBag, 'crit'

 The bag now contains two 'hit' and one 'crit' item.
 The number of items with the same value determines the longest streak (sequence) that can be drawn from the shuffle bag.
 Therefore, in the above example, the largest possible 'hit' streak is two, 'crit' streak is one.


### shuffleBagNext 
> shuffleBagNext  :: (ShuffleBag bag) -> Object

 Draws the next element from the shuffle bag, e.g.,

    if shuffleBagNext(@shuffleBag) is 'crit'
        hitCritical()

 If no items have been added previously, it returns undefined.



#  Debug




#  Position and Movement

 Each WorldObject has a position in the world.
 You can query the position and move the object somewhere else.

### unitGetPosition 
> unitGetPosition  :: (WorldObject unit) -> TerrainPosition

 Return the position at which the given object is located.
 The position is always valid.


### unitTeleportTo 
> unitTeleportTo  :: (WorldObject unit,  TerrainPosition  position) -> Event

 Creates a new event that teleports a unit to a new position.
 The only constraints are that the new position must be valid.
 No speed, line in sight checks etc are performed.
 The new position may even be in a completely new terrain.

 Use `eventSchedule` or `eventAppend` to apply the event.



#  Terrain

 Each game can have one or multiple terrains.
 All world objects are placed on and move along a terrain.

### terrainCreate 
> terrainCreate  :: (String name,  String  tag) -> undefined

 Create a new instance of a terrain. Each instance is identified by a unique tag.
 You can use this tag to refer to the instance.
 If your encounter has only one terrain, the convention is to use the `'default'` tag.
 You should create at least one terrain instance in the Glue constructor.
 Later during the game you can create additional instances if required.

 The tag must be unique.
 If your encounter uses multiple terrain instances, it?s up to you to make sure that the tags are unique.
 If you try to use a tag which already exists, the game will throw an exception.

    class Glue
        constructor: ->
            terrainCreate 'Maze', 'default'


### terrainGetPositionAt 
> terrainGetPositionAt  :: (String tag,  Number  x,  Number  y,  Number  z) -> TerrainPosition

 Create a `TerrainPosition` which represents the position at the x/y/z coordinates within the terrain instance identified by the tag.
 The z component does not need to be accurate.
 The function will project the position to the closests surface.

    pos = terrianGetPositionAt 'default', 0, 0, 0


### terrainPositionGetTile 
> terrainPositionGetTile  :: (TerrainPosition position) -> TerrainTile

 Returns the terrain tile the position belongs to.


### terrainPositionGetTerrain 
> terrainPositionGetTerrain  :: (TerrainPosition position) -> String

 Returns the tag of the terrain the position belongs to.


### terrainPositionSetFacing 
> terrainPositionSetFacing  :: (TerrainPosition position,  Number  lookat) -> TerrainPosition

 Returns a copy of the given position,
 with the facing direction changed to the given value.


### terrainTileGetPosition 
> terrainTileGetPosition  :: (TerrainTile tile,  Number  u,  Number  v) -> TerrainPosition

 Returns a terrain position from local coordinates within a tile.
 The local coordinates must be between 0 and 1.



#  WorldObject

 A WorldObject is an object which is located at a certain position within a terrain.
 Each WorldObject has a (non-unique) name, and a model associated which is used to render the object on the client.

### worldGetUnits 
> worldGetUnits  :: ( ) -> [WorldObject]

 The list of all objects in the world. You can use the `listFilter` function to
 filter these objects to select only those that you want. The following example
 gets a list of objects within 5 meters of self:
 
    targets = listFilter worldGetUnits(), (obj) ->
        distanceBetween(self, obj) < 5


### worldCreateUnit 
> worldCreateUnit  :: (String role,  String  name,  String  behavior,  TerrainPosition  position) -> WorldObject

 Create a new WorldObject. The name does not need to be unique.
 The role and behavior refer to the names of corresponding elements in the encounter editor.

    worldCreateUnit role, name, behavior, pos


### worldDeleteUnit 
> worldDeleteUnit  :: (WorldObject unit) -> undefined

 Remove the given WorldObject from the game.
 This causes the object to be immediately disappear on the client.



#  Spells and Cooldowns

 A WorldObject can cast only one spell at a time.
 Casting a spell may take some time, during that time the object may or may not move.
 Spells can be interrupted.
 Each spell is part of a cooldown group, all spells in that group share the same cooldown.
 Once a spell is successfully cast, no spell in the same cooldown group may be cast until the cooldown expires.

### unitTriggerCooldown 
> unitTriggerCooldown  :: (WorldObject unit,  String  cooldownName,  Number  cooldown) -> Event

 Creates an event that triggers the given cooldown category.
 The cooldown is given in seconds.
 A cooldown will prevent the object from casting spells in that cooldown category for the given amount of time.
 Many spells are in the GLOBAL cooldown category.
 This category usually has a short cooldown (1.5 seconds) and is used to prevent the player from casting spells rapidly after each other.

    event = unitTriggerCooldown self, 'GLOBAL', 1.5
    eventAppend e, event

 Use `eventSchedule` or `eventAppend` to apply the event.


### unitCooldownExpired 
> unitCooldownExpired  :: (WorldObject unit,  String  cooldownName) -> Boolean

 Returns true if the given cooldown category is not on cooldown.


### unitStartCast 
> unitStartCast  :: (WorldObject unit,  String  spellName,  WorldObject  target) -> Event

 Creates an event that starts the cast of a spell.

 Use `eventSchedule` or `eventAppend` to apply the event.


### unitStartCast 
> unitStartCast  :: (WorldObject unit) -> Event

 Creates an event that interrupts the cast of the currently cast spell.

 Use `eventSchedule` or `eventAppend` to apply the event.



#  Attributes

 Attributes are key/value pairs attached to a WorldObject.
 There are a few basic attributes, and you can also create your own.

 * `health`: When this attribute reaches zero then the WorldObject has died. This is displayed in the client UI as the health bar. The game engine will clamp this value between zero and `max-health`.
 * `max-health`: The maximum health that the unit can have.

### unitAttributeChangeBy 
> unitAttributeChangeBy  :: (WorldObject unit,  String  attribName,  Number  delta) -> Event

 Creates an event that changes the named attribute by the given delta.
 If the attribute does not exist, or is not a Number, then the game will throw an exception.

    event = unitAttributeChangeBy self, 'health', +10
    eventSchedule 5, event

 Use `eventSchedule` or `eventAppend` to apply the event.


### unitAttributeSet 
> unitAttributeSet  :: (WorldObject unit,  String  attribName,  Number  value) -> Event

 Creates an event that sets the attribute of a world object to the given value.

 Use `eventSchedule` or `eventAppend` to apply the event.


### unitAttributeGet 
> unitAttributeGet  :: (WorldObject unit,  String  attribName) -> undefined

 Returns the value of the given world object attribute.
 The example below sets the health to 50% of its current value.

    currentHealth = unitAttributeGet self, 'health'
    event         = unitAttributeSet self, 'health', currentHealth * 0.5
    eventSchedule 0, event



#  Appearance



### unitSetAppearance 
> unitSetAppearance  :: (WorldObject unit,  String  appearance) -> undefined

 Changes the unit appearance.



#  Auras

 Each WorldObject has a list of auras.
 The auras can strengthen or weaken the unit by accessing and modifying the combat log events during each tick.

### unitAuraAdd 
> unitAuraAdd  :: (WorldObject unit,  String  auraName) -> Event

 Creates an event that adds an aura to the given world object.

 Use `eventSchedule` or `eventAppend` to apply the event.


### unitAuraRemove 
> unitAuraRemove  :: (WorldObject unit,  String  auraName) -> Event

 Creates an event that removes an aura to the given world object.

 Use `eventSchedule` or `eventAppend` to apply the event.


### unitAuraTrigger 
> unitAuraTrigger  :: (WorldObject unit,  String  auraName) -> Event

 Creates an event that triggers an aura of the given world object.

 Use `eventSchedule` or `eventAppend` to apply the event.


### unitAuraIsPresent 
> unitAuraIsPresent  :: (WorldObject unit,  String  auraName) -> Boolean

 Returns true if the given world object has the given aura.



#  Parameters



### paramGet 
> paramGet  :: (Type type,  String  name) -> Object

 Returns the value of the given global parameter.
 Use the type parameter to ensure that the parameter is returned with the correct type.



#  Messages



### unitSpeak 
> unitSpeak  :: (WorldObject unit,  String  message) -> undefined

 Makes the given unit say something.



#  Misc



### distanceBetween 
> distanceBetween  :: (WorldObject x,  WorldObject  y) -> Number

 TODO: use some prefix and move it to the correct section.
 Returns the distance between the two world objects.


### isAlive 
> isAlive  :: (WorldObject worldObject) -> Boolean

 TODO: use some prefix and move it to the correct section.
 Returns wheter the given world object is alive.


### unitGetName 
> unitGetName  :: (WorldObject worldObject) -> String

 TODO: use some prefix and move it to the correct section.
 Returns the name of the given world object.


### hasOwnBehavior 
> hasOwnBehavior  :: (WorldObject worldObject) -> Boolean

 TODO: use some prefix and move it to the correct section.
 Returns wheter the given world object has a behavior (only NPC units have a behavior).



#  Lists



### listFilter 
> listFilter  :: ([Object] list,  Function  fn) -> [Object]

 Returns a copy of the given list, after it has been filtered.
 The filter function takes an element of the list and returns true if the object should be kept in the list.


### listSelectRandom 
> listSelectRandom  :: ([Object] list) -> Object

 Selects a random element from the list



