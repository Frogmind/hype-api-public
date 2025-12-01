# Component
## Summary
API for defining and managing Luau components attached to entities.

## Details
Components encapsulate reusable behavior and state that can be attached to entities.
Each component has a lifecycle managed by the engine:
- `onInit(...)`: Called when the component instance is constructed (initialize state, subscribe to events)
- `onStart()`: Called after all components have finished initialization (cross-component coordination)
- `onUpdate(deltaTime: number)`: Optional per-frame logic (requires subscription to update event)
- `onDestroy()`: Called before the component or its entity is destroyed (cleanup and unsubscribe)

Local Components run on the client.
Server Components run on the server. Toggle the execution context in the script node editor.

### Notes
- Keep component IDs stable; changing them breaks existing entity references.
- Use `onStart` for coordination with other components.

### Example
```luau
local ExampleLocalComponent = hype.component.define("example_component_id")

function ExampleLocalComponent:onInit(initialValue: number)
    self.value = initialValue
    -- Subscribe to engine update if you need per-frame logic
    self.onUpdateSub = hype.core.events.onUpdate(self, self.onUpdate)
end

function ExampleLocalComponent:onStart()
    -- Runs after all components finished onInit
end

function ExampleLocalComponent:onUpdate(deltaTime: number)
    -- Per-frame logic (only runs if you subscribed)
end

function ExampleLocalComponent:onDestroy()
    -- Unsubscribe / release references
    if self.onUpdateSub then
        self.onUpdateSub:unsubscribe()
        self.onUpdateSub = nil
    end
end

return ExampleLocalComponent
```

_Since: 0.1.0_

## API Reference

## define

Defines a Luau component by id.

### Signature

```luau
hype.component.define(id: string): LuauComponentDef
```

### Parameters
- id - unique component identifier

### Notes
- The returned table is the component "class"; instances inherit from it
- You can set optional lifecycle methods: onInit(self, ...), onStart(self), onDestroy(self)

### Example

```luau
local MyComp = hype.component.define("MyComp")
function MyComp.onInit(self, value)
  -- initialization
end
```

## getEntity

Returns the owning Entity of a component instance.

### Signature

```luau
hype.component.getEntity(componentInstance: ComponentInstance): Entity
```

### Parameters
- componentInstance - an instance previously created by the engine

### Notes
- Raises an error if the value is not a valid component instance

### Example

```luau
local entity = hype.component.getEntity(self)
```

## getDefId

Returns the component definition id.

### Signature

```luau
hype.component.getDefId(componentInstance: ComponentInstance): string
```
