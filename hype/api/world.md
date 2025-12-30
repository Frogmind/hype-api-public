# World
## Summary
Functions for interacting with the 3D world, such as spawning and destroying entities, playing audio, and querying world data.

## Details
Tags are case-insensitive strings assigned to entities for categorization and retrieval. It is good practice to add tags to entities for easier management.
Entities can have multiple tags, and tags can be added or removed at runtime.

## API Reference

## vibrate

Triggers a device vibration (haptic).

### Signature

```luau
hype.world.vibrate(type: string): ()
```

### Parameters
- type - one of: "Basic", "Impact", "Selection", "Success", "Warning", "Error", "Heavy", "Medium", "Light", "Rigid", "Soft"

### Notes
- Unrecognized names fall back to "Basic"

## isPlayer

Returns an integer player index when the entity belongs to a player; otherwise returns nil

### Signature

```luau
hype.world.isPlayer(entity: Entity): integer|nil
```

### Parameters
- entity - entity to check

## getTags

Returns all tags defined in the world

### Signature

```luau
hype.world.getTags(): {string}
```

## getEntitiesWithTag

Returns all entities with the given tag

### Signature

```luau
hype.world.getEntitiesWithTag(tag: string): {Entity}
```

## getGroundHeightAt

Returns ground height (y) at given position

### Signature

```luau
hype.world.getGroundHeightAt(position: Vector): number
```

## spawn

Spawns a copy of the given Entity into the world.

### Signature

```luau
hype.world.spawn(source: Entity, position: vector, rotation: vector?, scale: vector?): Entity
```

### Parameters
- source - entity to spawn
- position - spawn position (world or relative when parent provided)
- rotation - Quaternion rotation
- scale - uniform or per‑axis scale (default: (1,1,1))

### Notes
- Returns nil if spawning fails

### Example

```luau
local prefab = hype.asset.findPrefab("TreeLarge")
if prefab then
  local spawnedObject = hype.world.spawn(prefab, vector.create(0,0,0))
  if spawnedObject then
    -- do something with the spawned object
  end
end
```

## destroy

Destroys an entity instance in the world.

### Signature

```luau
hype.world.destroy(entity: Entity): ()
```

### Parameters
- entity - entity to remove

### Notes
- Does nothing if the entity is already destroyed or invalid
- Children are cleaned up automatically

## createEntity

Creates an empty entity in the world.

### Signature

```luau
hype.world.createEntity(position: vector?, rotation: vector?, scale: vector?): Entity
```

### Parameters
- position - optional spawn position (default: (0,0,0))
- rotation - optional Quaternion rotation (default: identity)
- scale - optional uniform or per‑axis scale (default: (1,1,1))

### Notes
- Attach visual and optionally physics components to make it visible and/or physical
