# Signal
## Summary
Decoupled messaging between components (local and remote).

## Details
Signals let components communicate without direct references. Two kinds of signals exist:
- Local Signals (hype.localSignal): confined to the current runtime (client only or server only).
- Remote Signals (hype.remoteSignal): travel between clients and the server.

You send a signal by (string) id plus optional routing fields and arbitrary payload arguments. Listeners subscribe
by the same id (and optional entity for local) and receive the payload when sent.

Local Use Cases:
- Cross‑component coordination (health changes, local UI updates).
- Zero network overhead and immediate delivery.

Remote Use Cases:
- Gameplay events that must be synchronized (score updates, state replication prompts).
- Client actions that the server must validate.

Best Practices:
- Keep ids short & consistent (PascalCase or snake_case).
- Avoid very high frequency remote signals; batch or throttle when possible.
- Prefer targeted filters on the server (playerIndex/include/exclude) to reduce bandwidth.

## API Reference

## send

Sends a local signal.

### Signature

```luau
hype.localSignal.send(filter: { id: string, entity: Entity? }, args: Tuple): ()
```

### Parameters
- filter - filter table with required field `id` and optional `entity` to restrict delivery to listeners bound to that entity.
- args - zero or more payload values delivered to subscribers.

### Notes
- Delivery is limited to the current runtime (no network).
- If `entity` is provided only subscribers specifying the same entity receive the signal.

### Example

```luau
hype.localSignal.send({ id = "HealthChanged", entity = self.entity }, newHealth, maxHealth)
```

## subscribe

Subscribes a component to a local signal.

### Signature

```luau
hype.localSignal.subscribe(filter: { id: string, entity: Entity? }, component: ComponentInstance, callback: (self: ComponentInstance, args: Tuple) -> ()): Subscription
```

### Parameters
- filter - table with required `id` and optional `entity`.
- component - owner; auto‑unsubscribes on destroy.
- callback - invoked with payload.

### Example

```luau
self.healthSub = hype.localSignal.subscribe({ id = "HealthChanged", entity = self.entity }, self, self.onHealthChanged)
```

## send

Sends a targeted remote signal.

### Signature

```luau
hype.remoteSignal.send(filter: { id: string, playerIndex: number?, includePlayers: { number }?, excludePlayers: { number }?, crossSession: boolean? }, args: Tuple): ()
```

### Parameters
- filter - required `id`; optionally exactly one of `playerIndex`, `includePlayers`, `excludePlayers` (server only). Host may set `crossSession = true`.
- args - payload values.

### Notes
- If no targeting field is given (server) all players receive the signal.
- Client omits targeting fields (sends to server).
- Use `includePlayers` to send to a specific set; `excludePlayers` for everyone except listed.

### Example

```luau
-- Server: send state to new player
hype.remoteSignal.send({ id = "GameState", playerIndex = player.playerIndex }, state)
```

## subscribe

Subscribes to a remote signal by id.

### Signature

```luau
hype.remoteSignal.subscribe(filter: { id: string }, component: ComponentInstance, callback: function): Subscription
```

### Parameters
- filter - required `id`.
- component - subscription owner.
- callback - Server signature

### Notes
- Player parameter is only provided on server side (originating player of the signal).

### Example

```luau
-- Client: subscribe to server updates
self.stateSub = hype.remoteSignal.subscribe({ id = "GameState" }, self, self.onGameState)
```
