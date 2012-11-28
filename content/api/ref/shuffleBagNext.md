---
title: API - Reference - shuffleBagNext
---

### shuffleBagNext :: (ShuffleBag) -> Any

Extracts and returns the next item of the shuffle bag, e.g.,

    if shuffleBagNext(@shuffleBag) is 'crit'
        hitCritical()

If no items have been added previously, it returns undefined.
