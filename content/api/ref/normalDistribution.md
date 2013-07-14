---
title: API - Reference - normalDistribution
---

### normalDistribution :: (Number, Number, Number) -> Number

Return a uniformly distributed random number. Because normal distribution has
no bounds, it's desirable to clamp the result to a specific range. The third
argument is used to specify the range (in the number of stddev multiplies
around the median).

## Example

Random number with median 10 and standard deviation 2. The result is clamped
to ± 6 (2*3) around the median. That means x will be always between 4 and 16.

    x = normalDistribution 10, 2, 3


## See Also

[uniformDistribution](/api/ref/uniformDistribution/),
[uniformSumDistribution](/api/ref/uniformSumDistribution/)


## References

 - [Normal distribution](http://en.wikipedia.org/wiki/Normal_distribution)
 - [Three-sigma rule](http://en.wikipedia.org/wiki/68-95-99.7_rule)
