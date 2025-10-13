# Entity

## API Reference

## getId

Returns the numeric id of the entity or raises an error if the entity is invalid.

### Signature

```luau
Entity:getId(): number
```

### Parameters
- self: Entity - the entity instance (implicit via colon syntax)

### Notes
- Returned id is an internal identifier; 0 is never returned (0 would mean invalid)
- An error is raised if the entity userdata is invalid / destroyed

### Example

```luau
local id = entity:getId()
print('Entity id', id)
```

## onCollisionStart

Subscribes to collision start events for this entity filtered by collision groups.

### Signature

```luau
Entity:onCollisionStart(groupFilter: {number}, component: LuauComponent, callback: function(component: LuauComponent, other: Entity?)): LuauSubscription
```

### Parameters
- self: Entity - the entity instance (implicit)
- groupFilter: {number} - list/array-style table of collision group indices to listen to (0-9)
- component: LuauComponent - component instance (table) receiving the callback
- callback: function(component: LuauComponent, other: Entity?) - called when a qualifying collision starts; other is the other entity or nil

### Notes
- Returns a LuauSubscription userdata; call subscription:unsubscribe() to stop receiving events
- groupFilter must contain valid collision group ids; invalid entries will cause an error
- The callback receives (component, otherEntity) exactly two arguments
- If other entity becomes invalid by the time of dispatch, other will be nil

### Example

```luau
local sub = entity:onCollisionStart({1,2}, self, function(selfComp, other)
    if other then print('Collision start with', other:getId()) end
end)
-- Later: sub:unsubscribe()
```

## onCollisionEnd

Subscribes to collision end events for this entity filtered by collision groups.

### Signature

```luau
Entity:onCollisionEnd(groupFilter: {number}, component: LuauComponent, callback: function(component: LuauComponent, other: Entity?)): LuauSubscription
```

### Parameters
- self: Entity - the entity instance (implicit)
- groupFilter: {number} - list/array-style table of collision group indices to listen to (0-9)
- component: LuauComponent - component instance (table) receiving the callback
- callback: function(component: LuauComponent, other: Entity?) - called when a qualifying collision ends; other is the other entity or nil

### Notes
- Returns a LuauSubscription userdata; call subscription:unsubscribe() to stop receiving events
- The callback receives (component, otherEntity) exactly two arguments

### Example

```luau
local sub = entity:onCollisionEnd({1,2}, self, function(selfComp, other)
    print('Collision ended with', other and other:getId())
end)
```

## getPosition

Returns the entity position as a vector.

### Signature

```luau
Entity:getPosition(global: boolean?): vector
```

### Parameters
- self: Entity - the entity instance (implicit)
- global: boolean? - if true returns global/world position; otherwise local (default: true)

## getRotation

Returns the entity rotation as Euler angles in degrees (vector order: x=pitch, y=yaw, z=roll).

### Signature

```luau
Entity:getRotation(): vector
```

### Parameters
- self: Entity - the entity instance (implicit)

### Notes
- The rotation is derived from the entity's internal quaternion
- Angle order is (pitch, yaw, roll)

### Example

```luau
local rot = entity:getRotation()
print('Yaw', rot.y)
```

## getRotation

Returns the entity rotation as a quaternion (vector4 x,y,z,w). Supports global or local space.

### Signature

```luau
Entity:getRotation(global: boolean?): rotation
```

### Parameters
- self: Entity - the entity instance (implicit)
- global: boolean? - if true returns global/world rotation; otherwise local rotation (default: true)

### Notes
- Quaternion order is (x, y, z, w)
- Use hype.math.toEuler(rotation) to convert to Euler angles if needed

### Example

```luau
local q = entity:getRotation()               -- world rotation as quaternion
local euler = hype.math.toEuler(q)           -- convert to Euler (radians)
```

## getDirection

Returns the forward direction vector of the entity (unit length).

### Signature

```luau
Entity:getDirection(): vector
```

### Parameters
- self: Entity - the entity instance (implicit)

### Notes
- Forward direction corresponds to the entity's -Z in world space
- Vector length should be ~1.0

### Example

```luau
local dir = entity:getDirection()
print(string.format("Direction: (%.2f, %.2f, %.2f)", dir.x, dir.y, dir.z))
```

## getSize

Returns the size of the entity as a vector (x = width, y = height, z = depth).

### Signature

```luau
Entity:getSize(visual: boolean?): vector
```

### Parameters
- self: Entity - the entity instance (implicit)
- visual: boolean? - if true (reserved) would return the visual/graphics size; otherwise the physical/collision size (default: false)

### Notes
- CURRENT BEHAVIOR: The implementation presently always returns the physical size; the visual argument is reserved for a future update.
- Size components are expressed in world units in the entity's local axis order.
- Physical size typically corresponds to the collision/physics bounding box extents.
- Passing any value for visual does not change the result yet; rely only on physical size for now.

### Example

```luau
local physSize = entity:getSize()            -- physical size (current behavior)
print('Physical size', physSize.x, physSize.y, physSize.z)
-- Future intention (not active yet): local visualSize = entity:getSize(true)
```

## setVisible

Sets the visibility of the entity; optionally applies to all child entities.

### Signature

```luau
Entity:setVisible(visible: boolean, includeChildren: boolean?): void
```

### Parameters
- self: Entity - the entity instance (implicit via colon syntax)
- visible: boolean - true to show, false to hide
- includeChildren: boolean? - if true, also applies to all children recursively (default: false)

### Notes
- This controls object visibility in the world. Physics is unaffected.
- When visibility changes, rendering and related systems are notified immediately.

### Example

```luau
entity:setVisible(false)            -- hide only this entity
entity:setVisible(true, true)       -- show this entity and all children
```
