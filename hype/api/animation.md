# Animation
## Summary
Skinned animation component access for entities.

## API Reference

## get

Returns this entity's animation component (skinned) or nil if none exists.

### Signature

```luau
hype.animation.get(entity: Entity): AnimationComponent?
```

### Parameters
- entity - the entity

## attach

Attaches a skinned animation component for the entity (if missing) and sets its animation by name.

### Signature

```luau
hype.animation.attach(entity: Entity, name: string): AnimationComponent
```

### Notes
- If the entity already has a skinned animation component, returns a handle to it and ignores the name.

## setAnimation

Changes the current animation by name.

### Signature

```luau
AnimationComponent:setAnimation(name: string): void
```

### Parameters
- name - animation clip name (fuzzy match)

## setSpeed

Sets the playback speed multiplier.

### Signature

```luau
AnimationComponent:setSpeed(speed: number): void
```

### Parameters
- speed - playback speed multiplier (capped internally)
