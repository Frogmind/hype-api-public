# Physics
## Summary
API for managing entitys physics.

## Details
Types:
- Type.Static: For objects that dont move, but can collide with dynamic objects
- Type.Kinematic: For objects that are moved by logic outside of physics simulation
- Type.Dynamic: For objects that are simulated by the physics engine

## API Reference

## addForce

Applies a linear impulse (or direct velocity change) to an entity's physics body.

### Signature

```luau
hype.physics.addForce(entity: Entity, force: vector, extraParams: { isLocal: boolean?, ignoreMass: boolean?, offset: vector?, maxSpeed: number? }?): ()
```

### Parameters
- entity - target entity
- force - impulse (NÂ·s) or velocity change if ignoreMass=true; ignored if near zero
- extraParams - optional parameters
  - extraParams.isLocal - interpret force (and offset) in local space (default
  - extraParams.ignoreMass - apply raw velocity change instead of impulse (default
  - extraParams.offset - point of application relative to entity origin (local if isLocal=true); adds torque (default
  - extraParams.maxSpeed - if > 0, caps the force so that the resulting speed will not go over maxSpeed along the force direction. Doesn't slow down the object if it's going
- faster than maxSpeed (default

### Notes
- Zero-length forces are ignored
- If offset is provided a torque impulse may also be generated
- When ignoreMass=true the provided vector is treated as Î”v (mass independent)

### Example

```luau
hype.physics.addForce(e, vector.create(0, 5, 0), { isLocal = true, offset = vector.create(0, 1, 0) })
```

## addTorque

Applies a torque impulse (or angular velocity change if ignoreMass = true) to an entity's physics body.

### Signature

```luau
hype.physics.addTorque(entity: Entity, torque: vector, extraParams: { isLocal: boolean?, ignoreMass: boolean? }?): ()
```

### Parameters
- entity - target entity
- torque - torque impulse (NÂ·mÂ·s); ignored if near zero
- extraParams - optional parameters
  - extraParams.isLocal - interpret torque in local space (default
  - extraParams.ignoreMass - apply angular velocity change directly (default

### Notes
- torque is ignored if near zero
- when isLocal=true, torque is in the entity's local space
- ignoreMass=true modifies angular velocity (not accumulated impulse)

### Example

```luau
hype.physics.addTorque(e, vector.create(0, 10, 0), { isLocal = true })
```

## overlapSphere

Returns entities whose colliders intersect a sphere.
{Entity}

### Signature

```luau
hype.physics.overlapSphere(position: vector, radius: number, extraParams: { groupFilter: {number}?, sortResultsByDistance: boolean?, ignoredEntities: {Entity}? }?):
```

### Parameters
- position - center of the sphere (world space)
- radius - sphere radius (> 0)
- extraParams - optional parameters
  - extraParams.groupFilter - collision groups to include (default
  - extraParams.sortResultsByDistance - sort ascending by squared distance from position (default
  - extraParams.ignoredEntities - entities to exclude

### Notes
- Returns an empty table if radius <= 0 or no overlaps
- Distance sort uses squared distance for performance

### Example

```luau
local hits = hype.physics.overlapSphere(vector.create(0,2,0), 1.5, { sortResultsByDistance = true })
```

## overlapBox

Returns entities whose colliders intersect an axis-aligned box.
{Entity}

### Signature

```luau
hype.physics.overlapBox(position: vector, halfSize: vector, extraParams: { groupFilter: {number}?, sortResultsByDistance: boolean?, ignoredEntities: {Entity}? }?):
```

### Parameters
- position - center of the box (world space)
- halfSize - half extents of the box (each component > 0)
- extraParams - optional parameters
  - extraParams.groupFilter - collision groups to include (default
  - extraParams.sortResultsByDistance - sort ascending by squared distance from position (default
  - extraParams.ignoredEntities - entities to exclude

### Notes
- Returns an empty table if any halfSize component <= 0 or no overlaps
- Box is axis-aligned (no rotation parameter yet)

### Example

```luau
local hits = hype.physics.overlapBox(vector.create(0,1,0), vector.create(1,2,1), { groupFilter = { 1, 3 } })
```

## setVelocity

Sets the entity's linear velocity.

### Signature

```luau
hype.physics.setVelocity(entity: Entity, velocity: vector, extraParams: { isLocal: boolean? }?): ()
```

## setAngularVelocity

Sets the entity's angular velocity (radians per second).

### Signature

```luau
hype.physics.setAngularVelocity(entity: Entity, angularVelocity: vector, extraParams: { isLocal: boolean? }?): ()
```

## attach

Attaches a physics component to the entity if missing and returns a handle.

### Signature

```luau
hype.physics.attach(entity: Entity, type: string?): EntityPhysics
```

### Parameters
- entity - target entity
- type - optional physics type

### Notes
- If the entity already has physics, returns a handle to it and ignores type.

## raycast

Casts a ray and returns a hit record (or an empty table if no hit).
Entity?, position: vector, normal: vector }? }

### Signature

```luau
hype.physics.raycast(origin: vector, ray: vector, extraParams: { groupFilter: {number}?, ignoreGroupFilter: {number}?, ignoredEntities: {Entity}? }?): { { entity:
```

### Parameters
- origin - ray start position (world space)
- ray - direction * length; length is |ray|; ignored if near zero
- extraParams - optional parameters
  - extraParams.groupFilter - groups to include (whitelist)
  - extraParams.ignoreGroupFilter - groups to exclude (blacklist)
  - extraParams.ignoredEntities - entities to skip

### Notes
- If both groupFilter and ignoreGroupFilter are provided, whitelist is applied first then blacklist
- Returns an empty table when no hit occurs
- Returned normal is unit length; position is world space

### Example

```luau
local hit = hype.physics.raycast(vector.create(0,2,0), vector.create(0,-5,0))
if hit.entity then print('Hit', hit.entity) end
```

## getPhysics

Returns a physics handle for the given entity or nil if not present.

### Signature

```luau
hype.physics.getPhysics(entity: Entity): EntityPhysics?
```

## getAllMaterials

Returns all physical materials available in the world.

### Signature

```luau
hype.physics.getAllMaterials(): {PhysicalMaterial}
```

## getMaterial

Returns a physical material by name or nil if not found.

### Signature

```luau
hype.physics.getMaterial(name: string): PhysicalMaterial?
```

## onCollisionStart

Subscribes to collision start events for this entity's physics, filtered by collision groups.

### Signature

```luau
EntityPhysics:onCollisionStart(groupFilter: {number}, component: LuauComponent, callback: (component: LuauComponent, other: Entity?): ()): LuauSubscription
```

### Parameters
- self - the physics handle (implicit)
- groupFilter - list/array-style table of collision group indices to listen to (0-9)
- component - component instance (table) receiving the callback
- callback - called when a qualifying collision starts; other is the other entity or nil

## onCollisionEnd

Subscribes to collision end events for this entity's physics, filtered by collision groups.

### Signature

```luau
EntityPhysics:onCollisionEnd(groupFilter: {number}, component: LuauComponent, callback: (component: LuauComponent, other: Entity?): ()): LuauSubscription
```

### Parameters
- self - the physics handle (implicit)
- groupFilter - list/array-style table of collision group indices to listen to (0-9)
- component - component instance (table) receiving the callback
- callback - called when a qualifying collision ends; other is the other entity or nil

## addForce

Applies a linear impulse (or direct velocity change) to an entity's physics body.

### Signature

```luau
Entity:addForce(force: vector, extraParams: { isLocal: boolean?, ignoreMass: boolean?, offset: vector?, maxSpeed: number? }?): ()
```

### Parameters
- force - impulse (NÂ·s) or velocity change if ignoreMass=true; ignored if near zero
- extraParams - optional parameters
  - extraParams.isLocal - interpret force (and offset) in local space (default
  - extraParams.ignoreMass - apply raw velocity change instead of impulse (default
  - extraParams.offset - point of application relative to entity origin (local if isLocal=true); adds torque (default
  - extraParams.maxSpeed - if > 0, caps resulting speed along the force direction; scales the applied force accordingly (default

### Notes
- Zero-length forces are ignored
- If offset is provided a torque impulse may also be generated
- When ignoreMass=true the provided vector is treated as Î”v (mass independent)

### Example

```luau
hype.physics.addForce(e, vector.create(0, 5, 0), { isLocal = true, offset = vector.create(0, 1, 0) })
```

## addTorque

Applies a torque impulse (or angular velocity change if ignoreMass = true) to an entity's physics body.

### Signature

```luau
Entity:addTorque(torque: vector, extraParams: { isLocal: boolean?, ignoreMass: boolean? }?): ()
```

### Parameters
- torque - torque impulse (NÂ·mÂ·s); ignored if near zero
- extraParams - optional parameters
  - extraParams.isLocal - interpret torque in local space (default
  - extraParams.ignoreMass - apply angular velocity change directly (default

### Notes
- torque is ignored if near zero
- when isLocal=true, torque is in the entity's local space
- ignoreMass=true modifies angular velocity (not accumulated impulse)

### Example

```luau
hype.physics.addTorque(e, vector.create(0, 10, 0), { isLocal = true })
```

## getVelocity

Gets the current linear velocity of the physics body.

### Signature

```luau
EntityPhysics:getVelocity(): vector
```

## setVelocity

Sets the current linear velocity of the physics body.

### Signature

```luau
EntityPhysics:setVelocity(velocity: vector, extraParams: { isLocal: boolean? }?): ()
```

## setAngularVelocity

Sets the current angular velocity of the physics body.

### Signature

```luau
EntityPhysics:setAngularVelocity(angularVelocity: vector, extraParams: { isLocal: boolean? }?): ()
```

## getId

Gets the unique id of this physical material.

### Signature

```luau
PhysicalMaterial:getId(): number
```

## getName

Gets the name of this physical material.

### Signature

```luau
PhysicalMaterial:getName(): string
```

## getDensity

Gets the density in kg-like units.

### Signature

```luau
PhysicalMaterial:getDensity(): number
```

## getRestitution

Gets the coefficient of restitution (bounciness).

### Signature

```luau
PhysicalMaterial:getRestitution(): number
```

## getFriction

Gets the friction coefficient.

### Signature

```luau
PhysicalMaterial:getFriction(): number
```

## getFrictionRolling

Gets the rolling friction coefficient.

### Signature

```luau
PhysicalMaterial:getFrictionRolling(): number
```

## getFrictionSpinning

Gets the spinning friction coefficient.

### Signature

```luau
PhysicalMaterial:getFrictionSpinning(): number
```

## getDampingAngular

Gets the angular damping factor.

### Signature

```luau
PhysicalMaterial:getDampingAngular(): number
```

## getDampingLinear

Gets the linear damping factor.

### Signature

```luau
PhysicalMaterial:getDampingLinear(): number
```

## getGravityMultiplier

Gets the gravity multiplier applied to bodies with this material.

### Signature

```luau
PhysicalMaterial:getGravityMultiplier(): number
```

## getSleepThresholdLinear

Gets the linear sleep threshold.

### Signature

```luau
PhysicalMaterial:getSleepThresholdLinear(): number
```

## getSleepThresholdAngular

Gets the angular sleep threshold.

### Signature

```luau
PhysicalMaterial:getSleepThresholdAngular(): number
```

## getFrictionAnisotropic

Gets the anisotropic friction vector (x,y,z multipliers).

### Signature

```luau
PhysicalMaterial:getFrictionAnisotropic(): vector
```

## setDensity

Sets the density. Values are clamped to [0.001, 10].

### Signature

```luau
PhysicalMaterial:setDensity(value: number): ()
```

## setRestitution

Sets the restitution (bounciness). Values are clamped to [0, 1].

### Signature

```luau
PhysicalMaterial:setRestitution(value: number): ()
```

## setFriction

Sets the friction coefficient. Values are clamped to [0, 10].

### Signature

```luau
PhysicalMaterial:setFriction(value: number): ()
```

## setFrictionRolling

Sets the rolling friction coefficient. Values are clamped to [0, 10].

### Signature

```luau
PhysicalMaterial:setFrictionRolling(value: number): ()
```

## setFrictionSpinning

Sets the spinning friction coefficient. Values are clamped to [0, 10].

### Signature

```luau
PhysicalMaterial:setFrictionSpinning(value: number): ()
```

## setDampingAngular

Sets the angular damping factor. Values are clamped to [0, 10].

### Signature

```luau
PhysicalMaterial:setDampingAngular(value: number): ()
```

## setDampingLinear

Sets the linear damping factor. Values are clamped to [0, 10].

### Signature

```luau
PhysicalMaterial:setDampingLinear(value: number): ()
```

## setGravityMultiplier

Sets gravity multiplier. Values are clamped to [0, 10].

### Signature

```luau
PhysicalMaterial:setGravityMultiplier(value: number): ()
```

## setSleepThresholdLinear

Sets linear sleep threshold. Values are clamped to [0, 10].

### Signature

```luau
PhysicalMaterial:setSleepThresholdLinear(value: number): ()
```

## setSleepThresholdAngular

Sets angular sleep threshold. Values are clamped to [0, 10].

### Signature

```luau
PhysicalMaterial:setSleepThresholdAngular(value: number): ()
```

## setFrictionAnisotropic

Sets anisotropic friction vector (x,y,z). Components are clamped to [0, 10].

### Signature

```luau
PhysicalMaterial:setFrictionAnisotropic(value: vector): ()
```
