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

## setLoop

Enables or disables looping for the current animation.

### Signature

```luau
AnimationComponent:setLoop(looping: boolean): void
```

### Parameters
- looping - true to loop, false to play once

## setSpeed

Sets the playback speed multiplier.

### Signature

```luau
AnimationComponent:setSpeed(speed: number): void
```

### Parameters
- speed - playback speed multiplier (capped internally)

## setScaleWithProportion

Scales the animation proportionally with character size.

### Signature

```luau
AnimationComponent:setScaleWithProportion(enabled: boolean): void
```

### Parameters
- enabled - true to scale with proportion

## setPosition

Sets the current animation position (0..1).

### Signature

```luau
AnimationComponent:setPosition(percent: number): void
```

### Parameters
- percent - normalized position in the animation
