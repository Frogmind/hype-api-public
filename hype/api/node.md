# Node
## Summary
API for defining custom script components (nodes) with typed inputs and outputs.

## Details
The node module lets Luau scripts expose inputs and outputs that integrate with the engine's visual scripting system.

TODO: Data Types and example and more details

## API Reference

## registerComponent

Registers a component definition as a node with inputs and outputs.

### Signature

```luau
hype.node.registerComponent(componentDef: ComponentDef, name: string, inputs: table, outputs: table): void
```

### Parameters
- componentDef - table returned by hype.component.define
- name - display name shown in editors / debug tools
- inputs - array of input definitions (name, type, default?, handler?)
- outputs - array of output definitions (name, type)

### Notes
- Must be called exactly once per component id.
- InputDef fields: name (string), type (DataType), default (any, optional), handler (function, optional)
- OutputDef fields: name (string), type (DataType)
- Returns nothing; raises on validation errors.

## pushOutput

Emits a value through a named output of a component instance.

### Signature

```luau
hype.node.pushOutput(component: LuauComponent, outputName: string, value: any)
```

### Parameters
- component - component instance (self)
- outputName - name declared in registerComponent outputs
- value - value matching the declared output type

### Notes
- Raises if the output name is unknown or the value type mismatches.
- Safe to call multiple times per frame.
