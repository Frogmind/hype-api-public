# Core

## API Reference

## onUpdate

Subscribes a callback that is invoked every frame for the given component instance.

### Signature

```luau
hype.core.events.onUpdate(component: ComponentInstance, callback: (component: ComponentInstance, dt: number): ()): Subscription
```

### Parameters
- component - the component instance whose update callback you want to receive
- callback - function called each frame; return value is ignored

### Notes
- dt is the frame delta time in seconds
- The callback is automatically unsubscribed when the component is destroyed
- You can manually unsubscribe early via the returned subscription: sub:unsubscribe()
- Execution order between different subscriptions is currently unspecified

### Example

```luau
local sub = hype.core.events.onUpdate(self, function(c, dt)
  -- Update logic here
end)
-- later, if desired
sub:unsubscribe()
```
