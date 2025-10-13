# Physics

## API Reference

## addForce

Applies a linear impulse (or direct velocity change) to an entity's physics body.

### Signature

```luau
hype.physics.addForce(entity: Entity, force: vector, extraParams: { isLocal: boolean?, ignoreMass: boolean?, offset: vector? }?): ()
```

### Parameters
- entity: Entity - target entity
- force: vector - impulse (N·s) or velocity change if ignoreMass=true; ignored if near zero
- extraParams: { isLocal: boolean?, ignoreMass: boolean?, offset: vector? }? - optional parameters
  - extraParams.isLocal: boolean? - interpret force (and offset) in local space (default: false)
  - extraParams.ignoreMass: boolean? - apply raw velocity change instead of impulse (default: false)
  - extraParams.offset: vector? - point of application relative to entity origin (local if isLocal=true); adds torque (default: nil)

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
hype.physics.addTorque(entity: Entity, torque: vector, extraParams: { isLocal: boolean?, ignoreMass: boolean? }?): ()
```

### Parameters
- entity: Entity - target entity
- torque: vector - torque impulse (N·m·s); ignored if near zero
- extraParams: { isLocal: boolean?, ignoreMass: boolean? }? - optional parameters
  - extraParams.isLocal: boolean? - interpret torque in local space (default: false)
  - extraParams.ignoreMass: boolean? - apply angular velocity change directly (default: false)

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
- position: vector - center of the sphere (world space)
- radius: number - sphere radius (> 0)
- extraParams: { groupFilter: {number}?, sortResultsByDistance: boolean?, ignoredEntities: {Entity}? }? - optional parameters
  - extraParams.groupFilter: {number}? - collision groups to include (default: all)
  - extraParams.sortResultsByDistance: boolean? - sort ascending by squared distance from position (default: false)
  - extraParams.ignoredEntities: {Entity}? - entities to exclude

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
- position: vector - center of the box (world space)
- halfSize: vector - half extents of the box (each component > 0)
- extraParams: { groupFilter: {number}?, sortResultsByDistance: boolean?, ignoredEntities: {Entity}? }? - optional parameters
  - extraParams.groupFilter: {number}? - collision groups to include (default: all)
  - extraParams.sortResultsByDistance: boolean? - sort ascending by squared distance from position (default: false)
  - extraParams.ignoredEntities: {Entity}? - entities to exclude

### Notes
- Returns an empty table if any halfSize component <= 0 or no overlaps
- Box is axis-aligned (no rotation parameter yet)

### Example

```luau
local hits = hype.physics.overlapBox(vector.create(0,1,0), vector.create(1,2,1), { groupFilter = { 1, 3 } })
```

## raycast

Casts a ray and returns a hit record (or an empty table if no hit).
Entity?, position: vector, normal: vector }? }

### Signature

```luau
hype.physics.raycast(origin: vector, ray: vector, extraParams: { groupFilter: {number}?, ignoreGroupFilter: {number}?, ignoredEntities: {Entity}? }?): { { entity:
```

### Parameters
- origin: vector - ray start position (world space)
- ray: vector - direction * length; length is |ray|; ignored if near zero
- extraParams: { groupFilter: {number}?, ignoreGroupFilter: {number}?, ignoredEntities: {Entity}? }? - optional parameters
  - extraParams.groupFilter: {number}? - groups to include (whitelist)
  - extraParams.ignoreGroupFilter: {number}? - groups to exclude (blacklist)
  - extraParams.ignoredEntities: {Entity}? - entities to skip

### Notes
- If both groupFilter and ignoreGroupFilter are provided, whitelist is applied first then blacklist
- Returns an empty table when no hit occurs
- Returned normal is unit length; position is world space

### Example

```luau
local hit = hype.physics.raycast(vector.create(0,2,0), vector.create(0,-5,0))
if hit.entity then print('Hit', hit.entity) end
```

## addForce

Applies a linear impulse (or direct velocity change) to an entity's physics body.

### Signature

```luau
Entity:addForce(force: vector, extraParams: { isLocal: boolean?, ignoreMass: boolean?, offset: vector? }?): ()
```

### Parameters
- force: vector - impulse (N·s) or velocity change if ignoreMass=true; ignored if near zero
- extraParams: { isLocal: boolean?, ignoreMass: boolean?, offset: vector? }? - optional parameters
  - extraParams.isLocal: boolean? - interpret force (and offset) in local space (default: false)
  - extraParams.ignoreMass: boolean? - apply raw velocity change instead of impulse (default: false)
  - extraParams.offset: vector? - point of application relative to entity origin (local if isLocal=true); adds torque (default: nil)

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
- torque: vector - torque impulse (N·m·s); ignored if near zero
- extraParams: { isLocal: boolean?, ignoreMass: boolean? }? - optional parameters
  - extraParams.isLocal: boolean? - interpret torque in local space (default: false)
  - extraParams.ignoreMass: boolean? - apply angular velocity change directly (default: false)

### Notes
- torque is ignored if near zero
- when isLocal=true, torque is in the entity's local space
- ignoreMass=true modifies angular velocity (not accumulated impulse)

### Example

```luau
hype.physics.addTorque(e, vector.create(0, 10, 0), { isLocal = true })
```
