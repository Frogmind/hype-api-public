# Visual
## Summary
Visual component and material access.

## Details
The `hype.visual` namespace exposes VisualComponent methods for controlling
an entity's rendering-related properties such as materials, visibility and
shadow casting.

Types:
- VisualComponent: Opaque handle for an entity's visual component.
- VisualMaterial: Opaque handle to a visual material resource.

## API Reference

## getMaterials

Returns the materials assigned to this visual component.

### Signature

```luau
VisualComponent:getMaterials(): {VisualMaterial}
```

### Notes
- Returns a list with up to 4 materials; empty slots are omitted.

## setMaterial

Sets a material to a specific slot.

### Signature

```luau
VisualComponent:setMaterial(material: VisualMaterial, slotIndex: number): void
```

### Parameters
- material - material handle to assign
- slotIndex - 0-based material slot index

## setVisible

Sets visibility of this visual component.

### Signature

```luau
VisualComponent:setVisible(visible: boolean): void
```

### Parameters
- visible - true to show, false to hide

## isVisible

Returns whether this visual component is visible.

### Signature

```luau
VisualComponent:isVisible(): boolean
```

## setCastShadow

Enables or disables dynamic shadow casting.

### Signature

```luau
VisualComponent:setCastShadow(enabled: boolean): void
```

### Parameters
- enabled - true to cast shadows dynamically, false to disable

## isCastShadow

Returns whether dynamic shadow casting is enabled.

### Signature

```luau
VisualComponent:isCastShadow(): boolean
```

## get

Gets the visual component of an entity.

### Signature

```luau
hype.visual.get(entity: entity): VisualComponent?
```

### Parameters
- entity - target entity whose visual component is queried

### Returns
The VisualComponent handle, or nil if the entity has no visual component

## attach

Create and return visual component for entity if it doesn't exist.

### Signature

```luau
hype.visual.attach(entity: entity, meshName: string, textureName: string): VisualComponent?
```

### Parameters
- entity to attach the visual component
- mesh resource name
- texture resource name

## getMaterial

Finds a visual material by name.

### Signature

```luau
hype.visual.getMaterial(name: string): VisualMaterial?
```

### Parameters
- name - material name (case-sensitive)

### Returns
The visual material handle, or nil if not found

## getAllMaterials

Returns all visual materials available in the world.

### Signature

```luau
hype.visual.getAllMaterials(): {VisualMaterial}
```

## getArtStyle

Finds an art style by name.

### Signature

```luau
hype.visual.getArtStyle(name: string): ArtStyle?
```

### Parameters
- name - art style name (case-sensitive)

### Returns
The art style handle, or nil if not found

## getCurrentArtStyle

Returns the currently applied art style, if any.

### Signature

```luau
hype.visual.getCurrentArtStyle(): ArtStyle?
```

## getAllArtStyles

Returns all art styles available in the world.

### Signature

```luau
hype.visual.getAllArtStyles(): {ArtStyle}
```

## changeModel

Copies the mesh/model from a source entity to this visual.

### Signature

```luau
VisualComponent:changeModel(source: entity): ()
```

### Parameters
- source - entity whose visual model acts as the donor

### Notes
- Updates the skinned-model flag and reinitializes/invalidates rigging if needed.
- Aligns position and rotation when both entities are glued under a non-logic parent.
- Does not modify physics or scale.

## changeMaterials

Copies materials from a source entity's visual to this visual.

### Signature

```luau
VisualComponent:changeMaterials(source: entity): ()
```

### Parameters
- source - entity whose visual materials act as the donor

### Notes
- Copies all material slots and the primary texture name.
- Emits visual property change notifications; does not modify physics.

## getId

Gets the unique id of this visual material.

### Signature

```luau
VisualMaterial:getId(): number
```

## getName

Gets the name of this visual material.

### Signature

```luau
VisualMaterial:getName(): string
```

## getColor

Gets the base color (RGBA).

### Signature

```luau
VisualMaterial:getColor(): vector
```

## getRoughness

Gets the surface roughness [0,1].

### Signature

```luau
VisualMaterial:getRoughness(): number
```

## getMetallic

Gets the metallic factor [0,1].

### Signature

```luau
VisualMaterial:getMetallic(): number
```

## getEmissive

Gets the emissive strength.

### Signature

```luau
VisualMaterial:getEmissive(): number
```

## getRim

Gets the rim lighting intensity [0,1].

### Signature

```luau
VisualMaterial:getRim(): number
```

## getTilingOffset

Gets the tiling offset.

### Signature

```luau
VisualMaterial:getTilingOffset(): { x: number, y: number }
```

## getTilingRepeat

Gets the tiling repeat (scale).

### Signature

```luau
VisualMaterial:getTilingRepeat(): { x: number, y: number }
```

## setColor

Sets the base color (RGBA).

### Signature

```luau
VisualMaterial:setColor(color: vector): ()
```

## setRoughness

Sets surface roughness. Clamped to [0,1].

### Signature

```luau
VisualMaterial:setRoughness(value: number): ()
```

## setMetallic

Sets metallic factor. Clamped to [0,1].

### Signature

```luau
VisualMaterial:setMetallic(value: number): ()
```

## setEmissive

Sets emissive strength. Clamped to [0,10].

### Signature

```luau
VisualMaterial:setEmissive(value: number): ()
```

## setRim

Sets rim lighting intensity. Clamped to [0,1].

### Signature

```luau
VisualMaterial:setRim(value: number): ()
```

## setTilingOffset

Sets tiling offset. Values wrap to [0,1).

### Signature

```luau
VisualMaterial:setTilingOffset({ x: number?, y: number? }): ()
```

## setTilingRepeat

Sets tiling repeat (scale). Each component clamped to [0,100].

### Signature

```luau
VisualMaterial:setTilingRepeat({ x: number?, y: number? }): ()
```

## getId

Gets the unique id of this art style.

### Signature

```luau
ArtStyle:getId(): number
```

## getName

Gets the name of this art style.

### Signature

```luau
ArtStyle:getName(): string
```

## apply

Applies this art style as the active world style.

### Signature

```luau
ArtStyle:apply(): ()
```

## getSunColor

Gets sun light color (RGBA).

### Signature

```luau
ArtStyle:getSunColor(): vector
```

## getSunIntensity

Gets sun light intensity.

### Signature

```luau
ArtStyle:getSunIntensity(): number
```

## getSunDirection

Gets sun rotation as quaternion (x,y,z,w).

### Signature

```luau
ArtStyle:getSunDirection(): vector
```

## getShowSunDisc

Returns whether the sun disc is visible.

### Signature

```luau
ArtStyle:getShowSunDisc(): boolean
```

## getSunDiscColor

Gets sun disc color (RGBA).

### Signature

```luau
ArtStyle:getSunDiscColor(): vector
```

## getSunDiscSize

Gets sun disc size.

### Signature

```luau
ArtStyle:getSunDiscSize(): number
```

## getSunGlow

Gets sun glow size.

### Signature

```luau
ArtStyle:getSunGlow(): number
```

## getExposure

Gets exposure value.

### Signature

```luau
ArtStyle:getExposure(): number
```

## getAmbientTopColor

Gets ambient top color (RGBA).

### Signature

```luau
ArtStyle:getAmbientTopColor(): vector
```

## getAmbientMiddleColor

Gets ambient middle color (RGBA).

### Signature

```luau
ArtStyle:getAmbientMiddleColor(): vector
```

## getAmbientBottomColor

Gets ambient bottom color (RGBA).

### Signature

```luau
ArtStyle:getAmbientBottomColor(): vector
```

## getAmbientGradientSoftness

Gets ambient gradient softness (top alpha).

### Signature

```luau
ArtStyle:getAmbientGradientSoftness(): number
```

## getAmbientIntensity

Gets ambient light intensity.

### Signature

```luau
ArtStyle:getAmbientIntensity(): number
```

## getSkyTopColor

Gets sky top color (RGBA).

### Signature

```luau
ArtStyle:getSkyTopColor(): vector
```

## getHorizonColor

Gets horizon color (RGBA).

### Signature

```luau
ArtStyle:getHorizonColor(): vector
```

## getBackgroundGradientSoftness

Gets background gradient softness (top alpha).

### Signature

```luau
ArtStyle:getBackgroundGradientSoftness(): number
```

## getHorizonHeight

Gets horizon height [-1,1].

### Signature

```luau
ArtStyle:getHorizonHeight(): number
```

## getSkyHorizontalRotation

Gets sky texture horizontal rotation in degrees.

### Signature

```luau
ArtStyle:getSkyHorizontalRotation(): number
```

## getStableHorizon

Returns whether horizon is stabilized at infinity.

### Signature

```luau
ArtStyle:getStableHorizon(): boolean
```

## getSkyBrightness

Gets sky brightness.

### Signature

```luau
ArtStyle:getSkyBrightness(): number
```

## getFogTintColor

Gets fog tint color (RGBA).

### Signature

```luau
ArtStyle:getFogTintColor(): vector
```

## getFogStart

Gets fog start distance.

### Signature

```luau
ArtStyle:getFogStart(): number
```

## getFogEnd

Gets fog end distance.

### Signature

```luau
ArtStyle:getFogEnd(): number
```

## getFogDensity

Gets fog density.

### Signature

```luau
ArtStyle:getFogDensity(): number
```

## getBloomIntensity

Gets bloom intensity.

### Signature

```luau
ArtStyle:getBloomIntensity(): number
```

## getBloomThreshold

Gets bloom threshold.

### Signature

```luau
ArtStyle:getBloomThreshold(): number
```

## getBloomSize

Gets bloom size [0,1].

### Signature

```luau
ArtStyle:getBloomSize(): number
```

## getToneMapMode

Gets tone map mode (NONE or ACES).

### Signature

```luau
ArtStyle:getToneMapMode(): string
```

## getVignetteStrength

Gets vignette strength [0,1].

### Signature

```luau
ArtStyle:getVignetteStrength(): number
```

## getVignetteThreshold

Gets vignette threshold [-1,1].

### Signature

```luau
ArtStyle:getVignetteThreshold(): number
```

## getVignetteColor

Gets vignette color (RGBA).

### Signature

```luau
ArtStyle:getVignetteColor(): vector
```

## getBrightness

Gets brightness adjustment [-1,1].

### Signature

```luau
ArtStyle:getBrightness(): number
```

## getSaturation

Gets saturation adjustment [-1,1].

### Signature

```luau
ArtStyle:getSaturation(): number
```

## getHighlights

Gets highlights adjustment [-1,1].

### Signature

```luau
ArtStyle:getHighlights(): number
```

## getShadows

Gets shadows adjustment [-1,1].

### Signature

```luau
ArtStyle:getShadows(): number
```

## getFilter

Gets color filter (None, Sepia, or Grayscale).

### Signature

```luau
ArtStyle:getFilter(): string
```

## getTintColor

Gets tint color (RGBA).

### Signature

```luau
ArtStyle:getTintColor(): vector
```

## getTintStrength

Gets tint strength [0,1].

### Signature

```luau
ArtStyle:getTintStrength(): number
```

## setSunColor

Sets sun light color (RGBA).

### Signature

```luau
ArtStyle:setSunColor(color: vector): ()
```

## setSunIntensity

Sets sun light intensity. Clamped to [0,1000].

### Signature

```luau
ArtStyle:setSunIntensity(value: number): ()
```

## setSunDirection

Sets sun rotation.

### Signature

```luau
ArtStyle:setSunDirection(rotation: quaternion): ()
```

## setShowSunDisc

Shows or hides the sun disc.

### Signature

```luau
ArtStyle:setShowSunDisc(enabled: boolean): ()
```

## setSunDiscColor

Sets sun disc color (RGBA).

### Signature

```luau
ArtStyle:setSunDiscColor(color: vector): ()
```

## setSunDiscSize

Sets sun disc size. Clamped to [0,2].

### Signature

```luau
ArtStyle:setSunDiscSize(value: number): ()
```

## setSunGlow

Sets sun glow size. Clamped to [0,1].

### Signature

```luau
ArtStyle:setSunGlow(value: number): ()
```

## setExposure

Sets exposure. Clamped to [0,10].

### Signature

```luau
ArtStyle:setExposure(value: number): ()
```

## setAmbientTopColor

Sets ambient top color (RGB). Alpha is used for gradient softness.

### Signature

```luau
ArtStyle:setAmbientTopColor(color: vector3): ()
```

## setAmbientMiddleColor

Sets ambient middle color (RGBA).

### Signature

```luau
ArtStyle:setAmbientMiddleColor(color: vector): ()
```

## setAmbientBottomColor

Sets ambient bottom color (RGBA).

### Signature

```luau
ArtStyle:setAmbientBottomColor(color: vector): ()
```

## setAmbientGradientSoftness

Sets ambient gradient softness. Clamped to [0.001,1].

### Signature

```luau
ArtStyle:setAmbientGradientSoftness(value: number): ()
```

## setAmbientIntensity

Sets ambient light intensity. Clamped to [0,100].

### Signature

```luau
ArtStyle:setAmbientIntensity(value: number): ()
```

## setSkyTopColor

Sets sky top color (RGB). Alpha is used for gradient softness.

### Signature

```luau
ArtStyle:setSkyTopColor(color: vector3): ()
```

## setHorizonColor

Sets horizon color (RGB). Alpha is used for horizon height.

### Signature

```luau
ArtStyle:setHorizonColor(color: vector3): ()
```

## setBackgroundGradientSoftness

Sets background gradient softness. Clamped to [0.001,1].

### Signature

```luau
ArtStyle:setBackgroundGradientSoftness(value: number): ()
```

## setHorizonHeight

Sets horizon height. Clamped to [-1,1].

### Signature

```luau
ArtStyle:setHorizonHeight(value: number): ()
```

## setSkyHorizontalRotation

Sets sky texture horizontal rotation (degrees). Clamped to [0,360].

### Signature

```luau
ArtStyle:setSkyHorizontalRotation(value: number): ()
```

## setStableHorizon

Enables or disables stabilized horizon at infinity.

### Signature

```luau
ArtStyle:setStableHorizon(enabled: boolean): ()
```

## setSkyBrightness

Sets sky brightness. Clamped to [0,100].

### Signature

```luau
ArtStyle:setSkyBrightness(value: number): ()
```

## setFogTintColor

Sets fog tint color (RGBA).

### Signature

```luau
ArtStyle:setFogTintColor(color: vector): ()
```

## setFogStart

Sets fog start distance. Clamped to [0, maxViewDistance] and <= fogEnd.

### Signature

```luau
ArtStyle:setFogStart(value: number): ()
```

## setFogEnd

Sets fog end distance. Clamped to [10, maxViewDistance] and >= fogStart.

### Signature

```luau
ArtStyle:setFogEnd(value: number): ()
```

## setFogDensity

Sets fog density. Clamped to [0.001,5].

### Signature

```luau
ArtStyle:setFogDensity(value: number): ()
```

## setBloomIntensity

Sets bloom intensity. Clamped to [0,100].

### Signature

```luau
ArtStyle:setBloomIntensity(value: number): ()
```

## setBloomThreshold

Sets bloom threshold. Clamped to [0,10].

### Signature

```luau
ArtStyle:setBloomThreshold(value: number): ()
```

## setBloomSize

Sets bloom size. Clamped to [0,1].

### Signature

```luau
ArtStyle:setBloomSize(value: number): ()
```

## setToneMapMode

Sets tone map mode (NONE or ACES).

### Signature

```luau
ArtStyle:setToneMapMode(mode: string): ()
```

## setVignetteStrength

Sets vignette strength. Clamped to [0,1].

### Signature

```luau
ArtStyle:setVignetteStrength(value: number): ()
```

## setVignetteThreshold

Sets vignette threshold. Clamped to [-1,1].

### Signature

```luau
ArtStyle:setVignetteThreshold(value: number): ()
```

## setVignetteColor

Sets vignette color (RGBA).

### Signature

```luau
ArtStyle:setVignetteColor(color: vector): ()
```

## setBrightness

Sets brightness adjustment. Clamped to [-1,1].

### Signature

```luau
ArtStyle:setBrightness(value: number): ()
```

## setSaturation

Sets saturation adjustment. Clamped to [-1,1].

### Signature

```luau
ArtStyle:setSaturation(value: number): ()
```

## setHighlights

Sets highlights adjustment. Clamped to [-1,1].

### Signature

```luau
ArtStyle:setHighlights(value: number): ()
```

## setShadows

Sets shadows adjustment. Clamped to [-1,1].

### Signature

```luau
ArtStyle:setShadows(value: number): ()
```

## setFilter

Sets color filter. One of: "None", "Sepia", or "Grayscale".

### Signature

```luau
ArtStyle:setFilter(name: string): ()
```

## setTintColor

Sets tint color (RGBA).

### Signature

```luau
ArtStyle:setTintColor(color: vector): ()
```

## setTintStrength

Sets tint strength. Clamped to [0,1].

### Signature

```luau
ArtStyle:setTintStrength(value: number): ()
```
