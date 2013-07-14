---
title: API - Reference - uniformSumDistribution
---

### uniformSumDistribution :: (Number, Number, Number) -> Number

Equivalent to running [uniformDistribution](/api/ref/uniformDistribution/)
N-times and adding the results.


## Example

Simulate a D&D type 4d6 roll (sum of four six-sided dice rolls):

    x = uniformSumDistribution 1, 6, 4


## See Also

[uniformDistribution](/api/ref/uniformDistribution/),
[normalDistribution](/api/ref/normalDistribution/)


## References

 - [UniformSumDistribution](http://mathworld.wolfram.com/UniformSumDistribution.html)
 - [Irwin-Hall Distribution](http://en.wikipedia.org/wiki/Irwin%E2%80%93Hall_distribution)
