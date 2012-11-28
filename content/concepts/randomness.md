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


## See Also

[random](/api/ref/random/),
[randomBetween](/api/ref/randomBetween/),
[randomIntBetween](/api/ref/randomIntBetween/),
[shuffleBagCreate](/api/ref/shuffleBagCreate/),
[shuffleBagAdd](/api/ref/shuffleBagAdd/),
[shuffleBagNext](/api/ref/shuffleBagNext/)

[Less-Random Generator]: http://seanmonstar.com/post/708989796/a-less-random-generator
