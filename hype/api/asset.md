# Asset

## API Reference

## findAudio

Finds an audio asset by name.

### Signature

```luau
hype.asset.findAudio(name: string): AudioAsset?
```

### Parameters
- name - audio asset name (case-sensitive)

### Returns
The found audio asset, or nil if no audio with the given name exists

## findPrefab

Finds a prefab asset by name.

### Signature

```luau
hype.asset.findPrefab(name: string): Entity?
```

### Returns
The found prefab's root entity, or nil if no prefab with the given name exists

### Notes
- -Use only if you know that the prefab already exists in the scene

## downloadPrefabById

Downloads a prefab by its unique ID.

### Signature

```luau
hype.asset.downloadPrefabById(id: string): Asset?
```

### Returns
The downloaded prefab's root entity, or nil if no prefab with the given name exists

### Notes
- Use only if you know the actual ID (name is not an id)
- Use findPrefab if you want to get already known prefab in the scene by name

## createPrefab

### Signature

```luau
hype.asset.createPrefab(name: string, root: Entity?): Entity
```
