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

## getById

Gets an asset by its unique ID.

### Signature

```luau
hype.asset.getById(id: string): Asset?
```

### Parameters
- id - The unique ID of the asset

## createPrefab

### Signature

```luau
hype.asset.createPrefab(name: string, root: Entity?): Entity
```
