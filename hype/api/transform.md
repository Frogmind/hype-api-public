# Transform
## Summary
API for translating, rotating and scaling entities at runtime.

## Details
Spaces:
- Space.Local: Relative to the entity's own local axes (only valid for delta style operations, NOT for setPosition / setRotation*)
- Space.Parent: Relative to the parent entity's coordinate space
- Space.World: In absolute world space

Tweening:
- Passing a duration > 0 starts an interpolated transform action.
- Tweening currently uses a linear easing (subject to future expansion).
- Passing duration <= 0 applies the change immediately.
- Optional cancelPrevious (boolean) cancels any existing transform action for the same entity before starting a new one (default: true).

Teleporting:
- Set isTeleport = true to disable visual interpolation for the current frame (snaps without smoothing).

Notes:
- setPosition / setRotation* in Local space is disallowed and will raise an error.
- setScale clamps scale components to a safe range to avoid numerical issues.

## API Reference

## translate

Translates an entity by delta in the given space.

### Signature

```luau
hype.transform.translate(entity: Entity, delta: vector, space: Space, duration: number?, isTeleport: boolean?, cancelPrevious: boolean?)
```

## rotate

Rotates an entity in the given space.

### Signature

```luau
hype.transform.rotate(entity: Entity, delta: Vector4, space: Space, duration: number?, isTeleport: boolean?, cancelPrevious: boolean?)
```

## setPosition

Sets the entity position in parent or world space.

### Signature

```luau
hype.transform.setPosition(entity: Entity, position: vector, space: Space, duration: number?, isTeleport: boolean?, cancelPrevious: boolean?)
```

### Notes
- Local space is invalid and raises an error.

## setRotationEuler

Sets the entity rotation using Euler angles.

### Signature

```luau
hype.transform.setRotationEuler(entity: Entity, rotation: vector, space: Space, duration: number?, isTeleport: boolean?, cancelPrevious: boolean?)
```

### Notes
- Prefer setRotation with a Quaternion to avoid gimbal issues.

## setRotation

Sets the entity rotation using a Quaternion.

### Signature

```luau
hype.transform.setRotation(entity: Entity, rotation: Vector4, space: Space, duration: number?, isTeleport: boolean?, cancelPrevious: boolean?)
```

## scale

Applies a relative scale delta to the entity.

### Signature

```luau
hype.transform.scale(entity: Entity, scale: vector, duration: number?, isTeleport: boolean?, cancelPrevious: boolean?)
```

## setScale

Sets the absolute scale of the entity.

### Signature

```luau
hype.transform.setScale(entity: Entity, scale: vector, duration: number?, isTeleport: boolean?, global: boolean?, cancelPrevious: boolean?)
```
