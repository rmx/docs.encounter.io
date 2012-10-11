---
title: encounter docs - "fair" random number generator
---

# "Fair" Random Number Generator

As discussed in many game designer communities (e.g. [Less-Random Generator]) a
"fair" less-random generator is preferable to avoid frustrating players, e.g.,
when having a 40% hit chance the player really expects to hit a creature twice
out of five swings. This kind of controlled randomness can be implemented with
a shuffle bag. A shuffle bag takes an arbitrary number of items, stuffs them
into a bag and shuffles the items. When a random item is requested an item is
drawn from the shuffle bag (and put aside). Once the bag is empty all items
will be inserted (again) and the bag is shuffled (again).


## Pseudo Random Number Generator

Designers can access an [Alea] PRNG by using the following symbols
in the script environment.

### random :: () -> Number

Returns a random value between [0,1].

    x = random()


### randomBetween :: (Number, Number) -> Number

Returns a random value between the two bounds.

    x = randomBetween 5, 10


### randomIntBetween :: (Number, Number) -> Number

Same as `randomBetween`, but rounds to a Integer.


## Shuffle Bag

Designers can use shuffle bags using the following symbols to get a freshly
created shuffle bag and apply operations.

### shuffleBagCreate :: () -> ShuffleBag

Returns a new (empty) shuffle bag.

    @shuffleBag = shuffleBagCreate()


### shuffleBagAdd :: (ShuffleBag, Any) -> undefined

Items can be added successively to a shuffle bag. The following example would
add three items to the shuffle bag.

    shuffleBagAdd @shuffleBag, 'hit'
    shuffleBagAdd @shuffleBag, 'hit'
    shuffleBagAdd @shuffleBag, 'crit'

The bag now contains two 'hit' and one 'crit' item. The number of items with
the same value determines the longest streak (sequence) that can be drawn from
the shuffle bag. Therefore, in the above example, the largest possible 'hit'
streak is two, 'crit' streak is one.


### shuffleBagNext :: (ShuffleBag) -> Any

Extracts and returns the next item of the shuffle bag, e.g.,

    if shuffleBagNext(@shuffleBag) is 'crit'
        hitCritical()

If no items have been added previously, it returns undefined.



[Less-Random Generator]: http://seanmonstar.com/post/708989796/a-less-random-generator
[Alea]: http://baagoe.com/en/RandomMusings/javascript/
