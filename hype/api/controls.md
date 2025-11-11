# Controls
## Summary
Player control access (buttons and joysticks).

## API Reference

## getJoysticks

Returns all joystick controls in the world.

### Signature

```luau
hype.controls.getJoysticks(): {controlsJoystick}
```

## getButtons

Returns all button controls in the world.

### Signature

```luau
hype.controls.getButtons(): {controlsButton}
```

## setColor

Sets the RGBA color override for a button control.

### Signature

```luau
controlsButton:setColor(color: vector4): ()
```

## setColor

Sets the RGBA color override for a joystick control.

### Signature

```luau
controlsJoystick:setColor(color: vector4): ()
```
