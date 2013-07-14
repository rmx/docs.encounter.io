---
title: Concept - Modifiers
---

# Modifiers

## castTime

<dl>
  <dt>Formula</dt>
  <dd>Standard Numeric Formula</dd>

  <dt>Application</dt>
  <dd>
    When calculating the effective spell castTime, this modifier is applied to
    the castTime base. The resulting value is clamped so it doesn't fall below
    the castTime minimum.
  </dd>
</dl>


## range

<dl>
  <dt>Formula</dt>
  <dd>Standard Numeric Formula</dd>

  <dt>Application</dt>
  <dd>
    This modifier applies to the spell range.
  </dd>
</dl>


## duration

<dl>
  <dt>Formula</dt>
  <dd>Standard Numeric Formula</dd>

  <dt>Application</dt>
  <dd>
    When an aura is added to a WorldObject the first time, this modifier is
    applied to its duration.

    It is unclear yet how this applies when the aura is refreshed.
  </dd>
</dl>


## tickInterval

<dl>
  <dt>Formula</dt>
  <dd>Standard Numeric Formula</dd>

  <dt>Application</dt>
  <dd>
    Same as the duration modifier.
  </dd>
</dl>


## globalCooldown

<dl>
  <dt>Formula</dt>
  <dd>Standard Numeric Formula</dd>

  <dt>Application</dt>
  <dd>
    When the global cooldown of a WorldObject is triggered, this modifier
    is applied to the duration.
  </dd>
</dl>


## maxHealth

<dl>
  <dt>Formula</dt>
  <dd>Standard Numeric Formula</dd>

  <dt>Application</dt>
  <dd>
    Changes the maximum health.
  </dd>
</dl>


## scale

<dl>
  <dt>Formula</dt>
  <dd>Standard Numeric Formula</dd>

  <dt>Application</dt>
  <dd>
    Applied to the WorldObject scale. Used to draw the model at the correct
    scale on the client.
  </dd>
</dl>


## movementSpeed

<dl>
  <dt>Formula</dt>
  <dd>Standard Numeric Formula</dd>

  <dt>Application</dt>
  <dd>
    Changes the base movement speed.
  </dd>
</dl>
