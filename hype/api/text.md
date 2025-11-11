# Text
## Summary
Text component access for entities.

## API Reference

## get

Returns entity's text component or nil if none exists.

### Signature

```luau
hype.text.get(entity: Entity): TextComponent?
```

### Parameters
- entity - the entity

## create

Creates a new 3D text at position.

### Signature

```luau
hype.text.create(position: vector, text: string): TextComponent?
```

### Parameters
- position - world position for the new text object
- text - initial text content

## getText

Returns current text content.

### Signature

```luau
TextComponent:getText(): string
```

## setText

Sets text content.

### Signature

```luau
TextComponent:setText(text: string): ()
```

### Parameters
- text - new text value

## isFacingCamera

Returns whether the text faces the camera (billboard).

### Signature

```luau
TextComponent:isFacingCamera(): boolean
```

## setFacingCamera

Sets whether the text faces the camera (billboard).

### Signature

```luau
TextComponent:setFacingCamera(enabled: boolean): ()
```

### Parameters
- enabled - true to enable billboard facing

## getColor

Gets the resolved color (RGBA).

### Signature

```luau
TextComponent:getColor(): vector4
```

## setColor

Sets the color override (RGBA).

### Signature

```luau
TextComponent:setColor(color: vector4): ()
```

### Parameters
- color - RGBA vector (0..1)

## getColorIndex

Gets the palette color index.

### Signature

```luau
TextComponent:getColorIndex(): number
```

## setColorIndex

Sets the palette color index.

### Signature

```luau
TextComponent:setColorIndex(index: number): ()
```

### Parameters
- index - color material index

## getStyle

Gets style (see CompUiText::STYLE). Returns one of "None", "Outline", "Bubble".

### Signature

```luau
TextComponent:getStyle(): string
```

## setStyle

Sets style (see CompUiText::STYLE).

### Signature

```luau
TextComponent:setStyle(style: string): ()
```

### Parameters
- style - one of "None", "Outline", "Bubble" (also accepts "STYLE_NONE", "STYLE_OUTLINE", "STYLE_BUBBLE")

## getSize

Gets size (see CompUiText::SIZE). Returns one of "Small", "Medium", "Large", "Tiny".

### Signature

```luau
TextComponent:getSize(): string
```

## setSize

Sets size (see CompUiText::SIZE).

### Signature

```luau
TextComponent:setSize(size: string): ()
```

### Parameters
- size - one of "Small", "Medium", "Large", "Tiny" (also accepts "SIZE_SMALL", "SIZE_MEDIUM", "SIZE_LARGE", "SIZE_TINY")

## isVisible

Returns visibility flag.

### Signature

```luau
TextComponent:isVisible(): boolean
```

## setVisible

Sets visibility flag (with transition handling).

### Signature

```luau
TextComponent:setVisible(visible: boolean): ()
```

## getHideAutomatically

Gets auto-hide flag.

### Signature

```luau
TextComponent:getHideAutomatically(): boolean
```

## setHideAutomatically

Sets auto-hide flag.

### Signature

```luau
TextComponent:setHideAutomatically(enabled: boolean): ()
```

## getTransition

Gets transition enum (see CompUiText::TRANSITION).

### Signature

```luau
TextComponent:getTransition(): number
```

## setTransition

Sets transition enum (see CompUiText::TRANSITION).

### Signature

```luau
TextComponent:setTransition(transition: number): ()
```

## getEntity

Returns the owning entity.

### Signature

```luau
TextComponent:getEntity(): Entity
```
