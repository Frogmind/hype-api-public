# Player
## Summary
API for accessing players and subscribing to player lifecycle events.

## Details
Players represent users connected to the current session. Each player is exposed as a table with immutable identity
fields and optional runtime state managed by the engine.

Player Events:
- onJoin: Fired when a player joins providing the new player.
- onLeave: Fired just before a player leaves providing the leaving player.

## API Reference

## onJoin

Subscribes a component to player join events.

### Signature

```luau
hype.player.events.onJoin(component: ComponentInstance, callback: (component: ComponentInstance, player: Player): ()): Subscription
```

### Parameters
- component: ComponentInstance - the component instance owning the subscription (used for auto-cleanup)
- callback: (component: ComponentInstance, player: Player): () - invoked when a player joins

### Example

```luau
self.joinSub = hype.player.events.onJoin(self, self.onPlayerJoin)
```

## onLeave

Subscribes a component to player leave events.

### Signature

```luau
hype.player.events.onLeave(component: ComponentInstance, callback: (component: ComponentInstance, player: Player): ()): Subscription
```

### Parameters
- component: ComponentInstance - the component instance owning the subscription
- callback: (component: ComponentInstance, player: Player): () - invoked when a player leaves

### Example

```luau
self.leaveSub = hype.player.events.onLeave(self, self.onPlayerLeave)
```

## getByIndex

Returns the player by absolute index.

### Signature

```luau
hype.player.getByIndex(index: number): Player?
```

### Parameters
- index: number - zero-based player index

### Notes
- Returns nil if no player with that index exists
- Indices are stable for the duration of a session

## getLocal

### Signature

```luau
hype.player.getLocal(): Player?
```

### Returns
Returns the local player.

### Notes
- On server, this will always return nil
- On client, returns the local user (or nil if not yet initialized)

### Example

```luau
local me = hype.player.getLocal()
if me then print("I am ", me.index) end
```

## registerSkin

Registers a player skin prefab for use by a player.

### Signature

```luau
hype.player.registerSkin(prefab: PrefabAsset): ()
```

### Parameters
- prefab: PrefabAsset - prefab containing the skin

### Example

```luau
local skinPrefab = hype.asset.findPrefab("MyPlayerSkin")
hype.player.registerSkin(skinPrefab)
```
