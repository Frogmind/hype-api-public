# Physics
## Summary
API for managing entity's physics.

## Details
Types:
- Type.Static: For entities that don't move, but can collide with physical entities
- Type.Kinematic: For entities that are moved by logic outside physics simulation
- Type.Dynamic: For entities that are simulated by the physics engine

## API Reference

## get

Gets the physics component handle for an entity, if present.

### Signature

```luau
hype.physics.get(entity: Entity): EntityPhysics?
```

### Parameters
- entity - target entity to query

### Returns
The EntityPhysics handle, or nil if the entity has no physics

## addForce

Applies a linear impulse (or direct velocity change) to an entity's physics body.

### Signature

```luau
hype.physics.addForce(entity: Entity, force: vector, extraParams: { isLocal: boolean?, ignoreMass: boolean?, offset: vector?, maxSpeed: number? }?): ()
```

### Parameters
- entity - target entity
- force - impulse (N·s) or velocity change if ignoreMass=true; ignored if near zero
- extraParams - optional parameters
  - extraParams.isLocal - interpret force (and offset) in local space (default: false)
  - extraParams.ignoreMass - apply raw velocity change instead of impulse (default: false)
  - extraParams.offset - point of application relative to entity origin (local if isLocal=true); adds torque (default: nil)
  - extraParams.maxSpeed - if > 0, caps the force so that the resulting speed will not go over maxSpeed along the force direction. Doesn't slow down the object if it's going
- faster than maxSpeed (default

### Notes
- Zero-length forces are ignored
- If offset is provided a torque impulse may also be generated
- When ignoreMass=true the provided vector is treated as Δv (mass independent)

### Example

```luau
hype.physics.addForce(e, vector.create(0, 5, 0), { isLocal = true, offset = vector.create(0, 1, 0) })
```

## explosiveForce

Applies an explosive impulse to nearby dynamic bodies.

### Signature

```luau
hype.physics.explosiveForce(position: vector, force: number, radius: number, fullForceRadius: number, maxSpeed: number?, groupFilter: {number}?): ()
```

### Parameters
- position - explosion center in world space
- force - impulse magnitude at the center
- radius - maximum radius where the impulse is applied
- fullForceRadius - inner radius with full force before falloff begins
- maxSpeed - optional linear speed cap applied after the impulse (default: no cap)
- groupFilter - optional collision groups to include (default: all)

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
  - extraParams.isLocal - interpret torque in local space (default: false)
  - extraParams.ignoreMass - apply angular velocity change directly (default: false)

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
  - extraParams.groupFilter - collision groups to include (default: all)
  - extraParams.sortResultsByDistance - sort ascending by squared distance from position (default: false)
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
  - extraParams.groupFilter - collision groups to include (default: all)
  - extraParams.sortResultsByDistance - sort ascending by squared distance from position (default: false)
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

## getGravity

Gets the current world gravity vector.

### Signature

```luau
hype.physics.getGravity(): vector
```

## setGravity

Sets the world gravity vector.

### Signature

```luau
hype.physics.setGravity(gravity: vector|number): ()
```

### Notes
- If a number is provided, it is interpreted as the Y component with X/Z set to 0.

## attach

Attaches a physics component to the entity if missing and returns a handle.

### Signature

```luau
hype.physics.attach(entity: Entity, type: Type?): EntityPhysics
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

## getType

Gets the physics type of this entity.

### Signature

```luau
EntityPhysics:getType(): Physics.Type
```

## setType

Sets the physics type of this entity.

### Signature

```luau
EntityPhysics:setType(type: Physics.Type): ()
```

## getMaterial

Gets the physical material index assigned to this entity.

### Signature

```luau
EntityPhysics:getMaterial(): number
```

## setMaterial

Sets the physical material.

### Signature

```luau
EntityPhysics:setMaterial(material: number|string): ()
```

### Notes
- Accepts a material index (number) or a material name (string).

## isActive

Returns whether the physics body is active in simulation.

### Signature

```luau
EntityPhysics:isActive(): boolean
```

## setActive

Activates or deactivates the physics body.

### Signature

```luau
EntityPhysics:setActive(active: boolean): ()
```

## isPreserveVelocity

Returns whether velocity is preserved when changing type.

### Signature

```luau
EntityPhysics:isPreserveVelocity(): boolean
```

## setPreserveVelocity

Sets whether to preserve velocity on type change. Not implemented.

### Signature

```luau
EntityPhysics:setPreserveVelocity(enabled: boolean): ()
```

## isSensor

Returns whether this body acts as a sensor (no physical response).

### Signature

```luau
EntityPhysics:isSensor(): boolean
```

## setSensor

Enables or disables sensor mode.

### Signature

```luau
EntityPhysics:setSensor(enabled: boolean): ()
```

## isStartSleeping

Returns whether the body should start sleeping.

### Signature

```luau
EntityPhysics:isStartSleeping(): boolean
```

## isLimitMovementX

Returns if linear movement along X is limited.

### Signature

```luau
EntityPhysics:isLimitMovementX(): boolean
```

## setLimitMovementX

Enables/disables linear movement limit along X.

### Signature

```luau
EntityPhysics:setLimitMovementX(enabled: boolean): ()
```

## isLimitMovementY

Returns if linear movement along Y is limited.

### Signature

```luau
EntityPhysics:isLimitMovementY(): boolean
```

## setLimitMovementY

Enables/disables linear movement limit along Y.

### Signature

```luau
EntityPhysics:setLimitMovementY(enabled: boolean): ()
```

## isLimitMovementZ

Returns if linear movement along Z is limited.

### Signature

```luau
EntityPhysics:isLimitMovementZ(): boolean
```

## setLimitMovementZ

Enables/disables linear movement limit along Z.

### Signature

```luau
EntityPhysics:setLimitMovementZ(enabled: boolean): ()
```

## isLimitTurningX

Returns if angular turning around X is limited.

### Signature

```luau
EntityPhysics:isLimitTurningX(): boolean
```

## setLimitTurningX

Enables/disables angular turning limit around X.

### Signature

```luau
EntityPhysics:setLimitTurningX(enabled: boolean): ()
```

## isLimitTurningY

Returns if angular turning around Y is limited.

### Signature

```luau
EntityPhysics:isLimitTurningY(): boolean
```

## setLimitTurningY

Enables/disables angular turning limit around Y.

### Signature

```luau
EntityPhysics:setLimitTurningY(enabled: boolean): ()
```

## isLimitTurningZ

Returns if angular turning around Z is limited.

### Signature

```luau
EntityPhysics:isLimitTurningZ(): boolean
```

## setLimitTurningZ

Enables/disables angular turning limit around Z.

### Signature

```luau
EntityPhysics:setLimitTurningZ(enabled: boolean): ()
```

## isScaledMass

Returns whether scaled mass is enabled.

### Signature

```luau
EntityPhysics:isScaledMass(): boolean
```

## setScaledMass

Enables/disables scaled mass. Not implemented.

### Signature

```luau
EntityPhysics:setScaledMass(enabled: boolean): ()
```

## isContinuousCollision

Returns whether continuous collision detection (CCD) is enabled.

### Signature

```luau
EntityPhysics:isContinuousCollision(): boolean
```

## setContinuousCollision

Enables/disables continuous collision detection (CCD).

### Signature

```luau
EntityPhysics:setContinuousCollision(enabled: boolean): ()
```

## isPhysicalParticle

Returns whether the body is treated as a physical particle.

### Signature

```luau
EntityPhysics:isPhysicalParticle(): boolean
```

## setPhysicalParticle

Enables/disables physical particle mode. Not implemented.

### Signature

```luau
EntityPhysics:setPhysicalParticle(enabled: boolean): ()
```

## isUltraQualityCollisions

Returns whether enhanced edge removal (ultra-quality collisions) is enabled.

### Signature

```luau
EntityPhysics:isUltraQualityCollisions(): boolean
```

## setUltraQualityCollisions

Enables/disables ultra-quality collisions. Not implemented.

### Signature

```luau
EntityPhysics:setUltraQualityCollisions(enabled: boolean): ()
```

## isAlwaysActive

Returns whether the body should always simulate (never sleep).

### Signature

```luau
EntityPhysics:isAlwaysActive(): boolean
```

## setAlwaysActive

Enables/disables always-active simulation. Not implemented.

### Signature

```luau
EntityPhysics:setAlwaysActive(enabled: boolean): ()
```

## getCollisionGroup

Gets the collision group index of the entity.

### Signature

```luau
EntityPhysics:getCollisionGroup(): number
```

## getCollideWith

Gets the list of collision groups this entity collides with.

### Signature

```luau
EntityPhysics:getCollideWith(): {number}
```

## changePhysics

Copies the physical resource (collision) from a source entity's visual to this entity and recreates physics if needed.

### Signature

```luau
EntityPhysics:changePhysics(source: Entity): ()
```

### Parameters
- source - entity whose visual's physical resource acts as the donor

### Notes
- If the entity is glued under a non-logic parent, the recreation is applied to the glued parent like in ModelSwitcher.
- Preserves stored physics state across recreation.

## onCollisionStart

Subscribes to collision start events for this entity's physics, filtered by collision groups.

### Signature

```luau
EntityPhysics:onCollisionStart(groupFilter: {number}, component: ComponentInstance, callback: (component: ComponentInstance, other: Entity?): ()): LuauSubscription
```

### Parameters
- self - the physics handle (implicit)
- groupFilter - list/array-style table of collision group indices to listen to (1-10)
- component - component instance (table) receiving the callback
- callback - called when a qualifying collision starts; other is the other entity or nil

## onCollisionEnd

Subscribes to collision end events for this entity's physics, filtered by collision groups.

### Signature

```luau
EntityPhysics:onCollisionEnd(groupFilter: {number}, component: ComponentInstance, callback: (component: ComponentInstance, other: Entity?): ()): LuauSubscription
```

### Parameters
- self - the physics handle (implicit)
- groupFilter - list/array-style table of collision group indices to listen to (1-10)
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
  - extraParams.isLocal - interpret force (and offset) in local space (default: false)
  - extraParams.ignoreMass - apply raw velocity change instead of impulse (default: false)
  - extraParams.offset - point of application relative to entity origin (local if isLocal=true); adds torque (default: nil)
  - extraParams.maxSpeed - if > 0, caps resulting speed along the force direction; scales the applied force accordingly (default: disabled)

### Notes
- Zero-length forces are ignored
- If offset is provided a torque impulse may also be generated
- When ignoreMass=true the provided vector is treated as Δv (mass independent)

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
  - extraParams.isLocal - interpret torque in local space (default: false)
  - extraParams.ignoreMass - apply angular velocity change directly (default: false)

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

## getAngularVelocity

Gets the current angular velocity of the physics body.

### Signature

```luau
EntityPhysics:getAngularVelocity(): vector
```

## getMass

Gets the mass of the physics body in kg-like units.

### Signature

```luau
EntityPhysics:getMass(): number
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
