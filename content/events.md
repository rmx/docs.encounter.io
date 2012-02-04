---
title: rmx docs - events
---

# Events

An event is a function name and arguments, which shall be called on a target
object at a certain point in the future. The event also includes information
about the origin and source objects. These are the objects which caused the
event to be generated.

You never directly create these events, but rather uses one of the many
wrappers that are available in a script context. This is to ensure that the
fields such as `source` and `origin` are properly set. It also makes it easier
because you don't have to worry about those.
