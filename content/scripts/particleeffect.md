---
title: encounter docs - particle effect
---

# Particle Effect

We implemented a particle engine based on the paradigm of
[SPARKS.js](https://github.com/zz85/sparks.js).
Particles are emitted from a source emitter with some specific characteristics
(denoted `initializers`), e.g.  color and size, and can be influenced with the
help of `modifiers`. As the name suggests the `initializers` affect the
particle properties at creation where `modifiers` are applied as particles age.


## Effect Specification

Particle effects are specified in JSON objects, e.g. the following implements
a simple particle effect:

    {
        "source": {
            "duration" : 2.0,
            "delay"    : 0.0
            "counter"  : "steady",
            "npart"    : 5000,
            "color"    : [265, 90, 90],
            "size"     : [1, 3],
            "offset"   : [0, 0, 0.8],
            "zone"     : { "SphereCapZone" : ["relunit label", 0.5, 0.6, 80] }
        },
        "initializers": [
            {"lifetime": [0.1, 0.4]}
        ],
        "modifiers": [
            {"age":  []},
            {"move": []},
            {"accelerate":  [0.0, 0.0, 0.5]},
            {"randomdrift": [0.1, 0.1, 0.1]}
        ]
    }

A particle effect has a `source` entry characterizing the particle emitter and
two lists of `initializers` and `modifiers`. In order to describe meaningful
positions in particle effects the definition distinguishes two position types:

* absolute (coordinates or unit), and
* relative (unit or labeled vertex).

For example in the effect definition above we have,

    "SphereCapZone": ["relunit label", 0.5, 0.6, 80]

The exact specification of the position is deferred to the spell script (more
specifically to the `particleEffectStart` call), where previously defined
position labels (`label`) are resolved to world objects, e.g.,

    particleEffectStart "name", {label: target}, {}

If not otherwise specified, the `self` label will always point to the
currently controlled unit. The next two sections discuss how particle effects
can be started and stopped.  Finally we discuss specialized effects like
projectiles, aura and ground area effects.


### particleEffectStart(name, settings) :: id

This script API function can be used to start a specific particle effect. The
`source` and `target` definition in the settings object is mandatory, e.g.:

    labels         = { source: self, target: target }
    settings       = { duration: 1.0 }
    part_effect_id = particleEffectStart 'name', labels, settings


### particleEffectStop(id) :: undefined

Can be used to stop a currently active particle effect with id `id`. This can
e.g. be used to stop a cast particle effect on spell interruption.


## Specialized Effects

In many situations we need simple projectiles (e.g. Frostbolt) or effects on
the ground floor. To simplify the life of the designers we added helper
methods to trigger these kind of effects without relying on using
`particleEffectStart` and `particleEffectStop`.


### groundAreaEffects(position, duration, radius, auraName, effectName) :: undefined

In many situations a spell may affect a certain area on the ground floor. To
accommodate for this situation we provide the `groundAreaEffect` API function.
The following call

    groundAreaEffect position, 20, 3, "Slow", "Ice Field"

creates a circular area of effect at the specified position with radius `3`
for `20` seconds. Additional to displaying the particle effect `Ice Field`,
the aura `Slow` is applied to every unit entering (and removed when leaving)
the area of effect.


### visualEffectName(name) :: undefined

To simplify particle effect on Aura ticks, we provide the `visualEffectName`
field in aura properties. The following line

    visualEffectName: "Stun"

starts the particle effect `Stun` when the aura ticks.


### projectile(speed, name) :: undefined

Using particle systems in projectiles (e.g. Frostbolt) can be simplified by
using the `projectile` property in the spell descriptor. The projectile takes
two arguments: its speed and name of the particle effect:

    projectile: { 10, "Frostbolt" }



## Zone

Zones are used to describe surfaces or volumes where particles are emitted or
modifiers are applied. The following zones are currently available:

* `CubeZone`
* `DiscZone`
* `LineZone`
* `PointZone`
* `ParallelogramZone`
* `SphereCapZone`

In the following we briefly introduce the arguments of these zones.


### "CubeZone": [position, x, y, z]

Creates a cube zone with origin `position` and `x` width, `y` depth and `z`
height.


### "DiscZone": [center, radiusNormal, outerRadius, innerRadius]

Creates a "2D" disc perpendicular to the specified `radiusNormal` around
`center` with the radius `outerRadius`. If an `innerRadius` is specified the
disc will a hole.


### "LineZone": [start, end]

Creates a line zone form `start` to `end` position.


### "PointZone": [position]

Creates a point zone in `position`.


### "ParallelogramZone": [corner, side1, side2]

Creates a rectangular like shape spanned from the origin in `corner` to both
side endpoints.


### "SphereCapZone": [origin, minr, maxr, phi]

Creates a half dome zone centered in the specified origin between `minr` and
`maxr` with an opening of `phi`



## Source

The source field completely specifies the particle emitter.

* `duration`: travel time to target (in seconds). Only used for projectiles
              and require a `target` field
* `delay`: start the particle effect with a delay (in seconds)
* `counter`: either `steady` (emits particles over time) or `shot` (emits all
             `npart` particles at once)
* `npart`: number of particles to emit
* `color`: color of the particle in HSV
* `size`: [min, max] size of particle
* `offset`: offset from `source`/`target` position if used
* `zone`:

The following arguments can be overridden by the settings object: `duration`,
`delay`, `counter`, `npart`, `color`, `size`, `offset`.


## Initializers

The available initializers are:

* `"lifetime": [min, max]`: lifetime of a particle
* `"velocity": [zone]`: set velocity according to position in zone
* `"radialvelocity": [outerRadius, innerRadius]`: helper to accelerate outward


## Modifiers

Some modifiers use TWEEN.js for interpolation. The default in all cases is
`linear.none`. See
[complete list](https://sole.github.com/tween.js/examples/03_graphs.html) for
available easing schemes.

At the moment we support the following modifiers:

* `"accelerate": [direction x, direction y, direction z]`: accelerate in
  specified 3D direction,
* `"acceleratefactor": [factor of velocity]`: accelerate based on `factor` of
  particles absolute velocity,
* `"acceleratevelocity": [factor based on velocity direction]`: adapt velocity
  by factor of velocity direction,
* `"age": [easing]`: age particle using tween easing (default: `linear.none`),
* `"colorshift": [target hue, target saturation, target value, easing]`:
  interpolate from particle color to target color using easing (default:
  linear),
* `"resize": [target min, target max, easing]`: interpolate from particle
  size to target particle size using easing (default: linear),
* `"move": []`: move particles, and
* `"randomdrift": [drift x, drift y, drift z]`: random drift by max. delta
  drift.

**Note**: If the particle effect has no `move` modifier the particles will not
move and the `age` is necessary for modifiers relying on the particle age.


## Deathzone

Deathzones can be used to remove particles traveling through a specific zone.
For example a rectangular zone can be used to block particles from traveling
through an opening or window.

Currently we only support `CubeZone` as deadzone (more will follow soon):

    "deathzone": { "CubeZone": [-50, -50, 0, 100, 100, -5] }

