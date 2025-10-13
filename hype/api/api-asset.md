# findAudio

## findAudio

Finds an audio asset by name (returns nil if not found).

### Signature

```luau
hype.asset.findAudio(name: string): AudioAsset?
```

### Parameters
- name: string - audio asset name (case-sensitive)

### Returns
The found audio asset, or nil if no audio with the given name exists

### Example

```luau
local sfx = hype.asset.findAudio("Explosion")
if sfx then
  -- play sfx
end
```

## findPrefab

Finds a prefab asset by name (returns nil if not found).

### Signature

```luau
hype.asset.findPrefab(name: string): PrefabAsset?
```

### Parameters
- name: string - prefab name (case-sensitive)

### Returns
The found prefab asset, or nil if no prefab with the given name exists

### Example

```luau
local prefab = hype.asset.findPrefab("TreeLarge")
if prefab then
  -- instantiate or inspect
end
```
