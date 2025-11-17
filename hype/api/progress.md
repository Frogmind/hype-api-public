# Progress
## Summary
Player progress and saved data API

## Details
Provides functions to persist player-related data.

## API Reference

## save

Saves a value under a namespaced key for the player.

### Signature

```luau
hype.progress.save(key: string, value: string|number|bool|vector|table|nil): ()
```

### Parameters
- key - identifier for the saved entry
- value - value to save

### Notes
- Passing nil as value deletes the saved entry for the given key.
- Tables with keys of type string or integer are supported. Other key types are ignored.

## load

Loads a previously saved value by key. Returns nil if not found.

### Signature

```luau
hype.progress.load(key: string): string|number|bool|vector|table|nil
```

### Parameters
- key - identifier for the saved entry
