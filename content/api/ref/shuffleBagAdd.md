---
title: API - Reference - shuffleBagAdd
---

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
