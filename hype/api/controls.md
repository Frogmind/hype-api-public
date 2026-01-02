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

## getJoystick

Finds a Joystick control on the given entity or its direct children.

### Signature

```luau
hype.controls.getJoystick(entity: Entity): controlsJoystick
```

## onStart

Subscribe to joystick touch start.

### Signature

```luau
controlsJoystick:onStart(component: ComponentInstance, callback: function(component: ComponentInstance, event: { source: joystickComponent })): Subscription
```

## onEnd

Subscribe to joystick touch end.

### Signature

```luau
controlsJoystick:onEnd(component: ComponentInstance, callback: function(component: ComponentInstance, event: { source: joystickComponent })): Subscription
```

## onMove

Subscribe to joystick movement updates.

### Signature

```luau
controlsJoystick:onMove(component: ComponentInstance, callback: function(component: ComponentInstance, event: { source: joystickComponent, magnitude: number, x: number, y: number, angle: number })): Subscription
```

## setColor

Sets the RGBA color override for a joystick control.

### Signature

```luau
controlsJoystick:setColor(color: vector4): ()
```

## setAppearance

Sets the visual appearance for a joystick control.
Accepted values: "Basic", "Arcade", "Minimal", "Shiny", "Plain", "Sci-fi", "None".

### Signature

```luau
controlsJoystick:setAppearance(appearance: string): ()
```

## setEnabled

Enables or disables the joystick.

### Signature

```luau
controlsJoystick:setEnabled(enabled: boolean): ()
```

## getEnabled

Returns whether the joystick is enabled.

### Signature

```luau
controlsJoystick:getEnabled(): boolean
```

## setAnalog

Sets analog mode (true) or digital (false).

### Signature

```luau
controlsJoystick:setAnalog(analog: boolean): ()
```

## getAnalog

Gets whether analog mode is enabled.

### Signature

```luau
controlsJoystick:getAnalog(): boolean
```

## setSmoothing

Enables or disables joystick smoothing.

### Signature

```luau
controlsJoystick:setSmoothing(enabled: boolean): ()
```

## getSmoothing

Returns whether smoothing is enabled.

### Signature

```luau
controlsJoystick:getSmoothing(): boolean
```

## setLockStartPosition

Locks initial touch position until release.

### Signature

```luau
controlsJoystick:setLockStartPosition(locked: boolean): ()
```

## getLockStartPosition

Returns whether start position is locked.

### Signature

```luau
controlsJoystick:getLockStartPosition(): boolean
```

## setDraggable

Allows dragging the joystick center while held.

### Signature

```luau
controlsJoystick:setDraggable(enabled: boolean): ()
```

## getDraggable

Returns whether dragging is enabled.

### Signature

```luau
controlsJoystick:getDraggable(): boolean
```

## setVisibility

Sets visibility behavior.

### Signature

```luau
controlsJoystick:setVisibility(visibility: string|number): ()
```

### Notes
- Accepted strings: VisibleAlways/VisibleOnTouch/Hidden

## getVisibility

Gets visibility behavior.

### Signature

```luau
controlsJoystick:getVisibility(): string|number
```

## setType

Sets joystick axis type.

### Signature

```luau
controlsJoystick:setType(type: string|number): ()
```

### Notes
- Accepted strings: XYAxis/XAxis/YAxis

## getType

Gets joystick axis type.

### Signature

```luau
controlsJoystick:getType(): string|number
```

## setAlignX

Sets horizontal screen alignment.

### Signature

```luau
controlsJoystick:setAlignX(align: string|number): ()
```

### Notes
- Accepted strings: Left/Center/Right

## getAlignX

Gets horizontal screen alignment.

### Signature

```luau
controlsJoystick:getAlignX(): string|number
```

## setAlignY

Sets vertical screen alignment.

### Signature

```luau
controlsJoystick:setAlignY(align: string|number): ()
```

### Notes
- Accepted strings: Top/Center/Bottom

## getAlignY

Gets vertical screen alignment.

### Signature

```luau
controlsJoystick:getAlignY(): string|number
```

## setTouchArea

Sets touch area.

### Signature

```luau
controlsJoystick:setTouchArea(area: string|number): ()
```

### Notes
- Accepted strings: Joystick/Expanded/HalfScreenHorizontally/Fullscreen/None

## getTouchArea

Gets touch area.

### Signature

```luau
controlsJoystick:getTouchArea(): string|number
```

## setScale

Sets joystick radius scale.

### Signature

```luau
controlsJoystick:setScale(scale: number): ()
```

### Notes
- Clamped to [0.333, 2.0]

## getScale

Gets joystick radius scale.

### Signature

```luau
controlsJoystick:getScale(): number
```

## setIconColor

Sets icon color override (RGBA).

### Signature

```luau
controlsJoystick:setIconColor(color: vector4): ()
```

## getIconColor

Gets resolved icon color.

### Signature

```luau
controlsJoystick:getIconColor(): vector4
```

## setIcon

Sets icon by name or enum.

### Signature

```luau
controlsJoystick:setIcon(icon: string|number): ()
```

### Notes
- Accepted strings: None/Move/Jump/Interact/Attack/Shoot/Drive/Boost/Settings/ArrowUp/ArrowRight/ArrowDown/ArrowLeft/OpenArrowUp/OpenArrowRight/OpenArrowDown/OpenArrowLeft

## getIcon

Gets current icon as string when known (otherwise number).

### Signature

```luau
controlsJoystick:getIcon(): string|number
```

## getId

Returns the component id associated with this handle.

### Signature

```luau
controlsJoystick:getId(): number
```

## setKeyboard1Left

Maps a keyboard/mouse primary button for left.

### Signature

```luau
controlsJoystick:setKeyboard1Left(name: string): ()
```

## setKeyboard2Left

Maps a keyboard/mouse secondary button for left.

### Signature

```luau
controlsJoystick:setKeyboard2Left(name: string): ()
```

## setControllerLeft

Maps a gamepad button for left.

### Signature

```luau
controlsJoystick:setControllerLeft(name: string): ()
```

## setKeyboard1Right

Maps a keyboard/mouse primary button for right.

### Signature

```luau
controlsJoystick:setKeyboard1Right(name: string): ()
```

## setKeyboard2Right

Maps a keyboard/mouse secondary button for right.

### Signature

```luau
controlsJoystick:setKeyboard2Right(name: string): ()
```

## setControllerRight

Maps a gamepad button for right.

### Signature

```luau
controlsJoystick:setControllerRight(name: string): ()
```

## setKeyboard1Up

Maps a keyboard/mouse primary button for up.

### Signature

```luau
controlsJoystick:setKeyboard1Up(name: string): ()
```

## setKeyboard2Up

Maps a keyboard/mouse secondary button for up.

### Signature

```luau
controlsJoystick:setKeyboard2Up(name: string): ()
```

## setControllerUp

Maps a gamepad button for up.

### Signature

```luau
controlsJoystick:setControllerUp(name: string): ()
```

## setKeyboard1Down

Maps a keyboard/mouse primary button for down.

### Signature

```luau
controlsJoystick:setKeyboard1Down(name: string): ()
```

## setKeyboard2Down

Maps a keyboard/mouse secondary button for down.

### Signature

```luau
controlsJoystick:setKeyboard2Down(name: string): ()
```

## setControllerDown

Maps a gamepad button for down.

### Signature

```luau
controlsJoystick:setControllerDown(name: string): ()
```
