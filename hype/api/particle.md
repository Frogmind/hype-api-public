# Particle
## Summary
Particle component access for entities.

## API Reference

## get

Returns this entity's particle component or nil if none exists.

### Signature

```luau
hype.particle.get(entity: Entity): ParticleComponent?
```

### Parameters
- entity - the entity

## setEnabled

Enables or disables particle emission.

### Signature

```luau
ParticleComponent:setEnabled(enabled: boolean): void
```

## isEnabled

Returns whether particle emission is enabled.

### Signature

```luau
ParticleComponent:isEnabled(): boolean
```

## setOffset

Sets particle offset vector.

### Signature

```luau
ParticleComponent:setOffset(offset: vector): void
```

## getOffset

Gets particle offset vector.

### Signature

```luau
ParticleComponent:getOffset(): vector
```

## setTargetEntity

Sets the target entity whose transform drives the particle effect.

### Signature

```luau
ParticleComponent:setTargetEntity(target: Entity|nil): void
```

### Parameters
- target - entity to follow; pass nil to reset to self

## getTargetEntity

Gets the current target entity or nil if self.

### Signature

```luau
ParticleComponent:getTargetEntity(): Entity?
```

## setExecuting

Enables or disables emission execution.

### Signature

```luau
ParticleComponent:setExecuting(enabled: boolean): void
```

## isExecuting

Returns whether particle emission executes.

### Signature

```luau
ParticleComponent:isExecuting(): boolean
```

## setScaleWithObject

Toggles scaling the offset by the owning object's scale.

### Signature

```luau
ParticleComponent:setScaleWithObject(enabled: boolean): void
```

## isScaleWithObject

Returns whether particle offset scales with object.

### Signature

```luau
ParticleComponent:isScaleWithObject(): boolean
```

## setEffect

Sets the particle effect by name.

### Signature

```luau
ParticleComponent:setEffect(name: string): void
```

### Notes
- Name must match a loaded particle group; otherwise no change

## getEffect

Gets current particle effect name.

### Signature

```luau
ParticleComponent:getEffect(): string?
```

## setOffsetType

Sets offset space.

### Signature

```luau
ParticleComponent:setOffsetType(type: string): void
```

### Parameters
- type - "Global" or "Local"

## getOffsetType

Gets current offset type name.

### Signature

```luau
ParticleComponent:getOffsetType(): string
```
