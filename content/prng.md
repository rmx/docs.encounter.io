---
title: rmx docs - "fair" random number generator
---

# "Fair" Random Number Generator

As discussed in many game designer communities (e.g. [Less-RandomGenerator]) a
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

### random :: Number

Returns a random value between [0,1].

### randomBetween(min, max) :: Number

Returns a random value between [min, max].

### randomIntBetween(min, max) :: Number

Returns a random integer value between [min, max].


## Shuffle Bag

Designers can use shuffle bags using the following symbols to get a freshly
created shuffle bag and apply operations.

### newShuffleBag :: ShuffleBag

Returns a new (empty) shuffle bag.

    @shuffleBag = $newShuffleBag()

### add (items, repetition = 1) :: undefined

Items can be added successively to a shuffle bag and an optional repetition
frequency can be specified. After performing

    @shuffleBag.add ['hit', 'crit']
    @shuffleBag.add ['hit', 'crit'], 2

on an empty shuffle bag, the bag contains three 'hit' and three 'crit' items.
The number of items with the same value determines the longest streak
(sequence) that can be drawn from the shuffle bag. Therefore, in the above
example, the largest possible 'hit' or 'crit' streak has length 3.


### addBag (bag) :: undefined

Adds the items of one shuffle bag into another:

    @shuffleBag.addBag bag


### next :: polymorphic

Extracts and returns the next item of the shuffle bag, e.g.,

    if @shuffleBag.next() is 'crit'
        hitCritical()

If no items have been added previously, next returns undefined.



[Less-RandomGenerator]: http://seanmonstar.com/post/708989796/a-less-random-generator
[Alea]: http://baagoe.com/en/RandomMusings/javascript/
