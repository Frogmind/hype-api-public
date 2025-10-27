# World

## API Reference

## playAudio

Plays an audio asset (music or one‑shot SFX).

### Signature

```luau
hype.world.playAudio(audio: AudioAsset|integer): ()
```

### Parameters
- audio - handle returned by hype.asset.findAudio

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

Spawns a copy of the given Entity into the world.

### Signature

```luau
hype.world.spawn(source: Entity, position: vector, rotation: vector?, scale: vector?): Entity
```

### Parameters
- source - entity to spawn
- position - spawn position (world or relative when parent provided)
- rotation - Quaternion rotation
- scale - uniform or per‑axis scale (default

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

### Example

```luau
local e = someSpawnedEntity
hype.world.destroy(e)
```
