# World

## API Reference

## playAudio

Plays an audio asset (music or one‑shot SFX).

### Signature

```luau
hype.world.playAudio(audio: AudioAsset|integer): ()
```

### Parameters
- audio: AudioAsset|integer - handle returned by hype.asset.findAudio

### Notes
- For streaming (music) assets: plays once (non-looping) currently
- For SFX assets: creates a transient one‑shot that auto releases
- Silently does nothing if the asset id is invalid

### Example

```luau
local explosionAudio = hype.asset.findAudio("Explosion")
if explosionAudio then
  hype.world.playAudio(explosionAudio)
end
```

## spawn

Spawns a copy of the given Entity or prefab into the world.

### Signature

```luau
hype.world.spawn(source: Entity | PrefabAsset, parent: Entity?, boneName: string?, position: vector, scale: vector?, rotation: vector?): {Entity}
```

### Parameters
- source: Entity - entity or prefab to spawn
- parent: Entity? - optional parent entity to attach to
- boneName: string? - optional bone/socket name on the parent
- position: vector - spawn position (world or relative when parent provided)
- scale: vector? - uniform or per‑axis scale (default: (1,1,1))
- rotation: vector? - Euler XYZ rotation in degrees (default: (0,0,0))

### Notes
- Returns nil if spawning fails
- Rotation currently accepts Euler angles; quaternion support may be added later
- Result is an array of spawned entities (root first)

### Example

```luau
local prefab = hype.asset.findPrefab("TreeLarge")
if prefab then
  local spawned = hype.world.spawn(prefab, nil, nil, vector.create(0,0,0))
  if spawned then
    local root = spawned[1]
    -- manipulate root
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
- entity: Entity - entity to remove

### Notes
- Does nothing if the entity is already destroyed or invalid
- Children are cleaned up automatically

### Example

```luau
local e = someSpawnedEntity
hype.world.destroy(e)
```
