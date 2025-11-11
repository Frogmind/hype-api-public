# Progress
## Summary
Player progress and saved data API (stub).

## Details
Provides functions to persist player-related data. This is currently a
placeholder and may change; the implementation is a no-op for now.

## API Reference

## save

Saves a value under a namespaced key for the player.

### Signature

```luau
hype.progress.save(key: string, value: table): ()
```

### Parameters
- key - identifier for the saved entry
- value - table payload to be stored

## load

Loads a previously saved table by key. Returns nil if not found.

### Signature

```luau
hype.progress.load(key: string): table?
```

### Parameters
- key - identifier for the saved entry
