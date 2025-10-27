# Entity

## API Reference

## getId

Returns the numeric id of the entity or raises an error if the entity is invalid.

### Signature

```luau
Entity:getId(): number
```

### Parameters
- self - the entity (implicit)

### Notes
- Returned id is an internal identifier; 0 is never returned (0 would mean invalid)
- An error is raised if the entity userdata is invalid / destroyed

### Example

```luau
local id = entity:getId()
print('Entity id', id)
```

## getPosition

Returns the entity position as a vector.

### Signature

```luau
Entity:getPosition(global: boolean?): vector
```

### Parameters
- self - the entity (implicit)
- global - if true returns global/world position; otherwise local (default

## getRotation

Returns the entity rotation as Euler angles in radians.

### Signature

```luau
Entity:getRotation(): vector
```

### Parameters
- self - the entity (implicit)

## getRotation

Returns the entity rotation as a quaternion (vector x,y,z,w).

### Signature

```luau
Entity:getRotation(global: boolean?): rotation
```

### Parameters
- self - the entity (implicit)
- global - if true returns global/world rotation; otherwise local rotation (default

### Notes
- Quaternion order is (x, y, z, w)
- Use hype.math.toEuler(rotation) to convert to Euler angles if needed

### Example

```luau
local q = entity:getRotation()               -- world rotation as quaternion
local euler = hype.math.toEuler(q)           -- convert to Euler (radians)
```

## getScale

Returns the entity scale vector.

### Signature

```luau
Entity:getScale(global: boolean?): vector
```

### Parameters
- self - the entity (implicit)
- global - if true returns global/world scale; otherwise local scale (default

### Notes
- Global scale is derived by multiplying this entity's local scale by all parent scales.
- Components are clamped to a minimum internally to avoid zero scale issues.

## getDirection

Returns the forward direction vector of the entity (unit length).

### Signature

```luau
Entity:getDirection(): vector
```

### Parameters
- self - the entity (implicit)

### Notes
- Forward direction corresponds to the entity's -Z in world space

## getDimensions

Returns the dimensions of the entity as a vector (x = width, y = height, z = depth).
local dims = myPrefab:getDimensions()
local offset = myPrefab:getCenterOfBoundingBox()
-- Spawn prefab on the ground
local y = groundY + dims.y * 0.5 - offset.y
hype.world.spawn(myPrefab, vector.create(0, y, 0))

### Signature

```luau
Entity:getDimensions(): vector
```

### Parameters
- self - the entity (implicit)

### Notes
- When you want to spawn entities on the ground or relative to other entities, use this and the `getCenterOfBoundingBox` method to position entities correctly

## getCenterOfBoundingBox

Returns the coordinates of the center of the entity's bounding box in the entity's local coordinate system

### Signature

```luau
Entity:getCenterOfBoundingBox(): vector
```

### Parameters
- self - the entity (implicit)

## getPhysics

Returns the physics component for this entity or nil if it has no physics component.

### Signature

```luau
Entity:getPhysics(): PhysicsComponent?
```

### Parameters
- self - the entity (implicit)

## setVisible

Sets the visibility of the entity; optionally applies to all child entities.

### Signature

```luau
Entity:setVisible(visible: boolean, includeChildren: boolean?): void
```

### Parameters
- self - the entity (implicit)
- visible - true to show, false to hide
- includeChildren - if true, also applies to all children recursively (default

### Notes
- Physics is unaffected.

## getParent

Returns the parent entity or nil if this is a root or invalid entity.

### Signature

```luau
Entity:getParent(): Entity?
```

### Parameters
- self - the entity (implicit)

## getChildren

Returns a list-style table of this entity's direct children.

### Signature

```luau
Entity:getChildren(): {Entity}
```

### Parameters
- self - the entity (implicit)

### Example

```luau
for i, child in ipairs(entity:getChildren()) do
    -- Do something with child
end
```

## attachComponent

Attaches a component to an entity.

### Signature

```luau
entity:attachComponent(componentDef: ComponentDef|string, initArgs: Tuple): ComponentInstance?
```

### Parameters
- self - the entity (implicit)
- componentDef - id of a previously defined component via hype.component.define(...) or a ComponentDef
- initArgs - zero or more values forwarded to the component's onInit(...) (if defined)

### Notes
- The component definition must be registered before (hype.component.define). An error is raised if not found.
- Initialization arguments after componentDef are collected and passed in order when constructing the component instance (available inside onInit via its parameters).
- Currently, attaching components on prefab entities does not support initArgs. Do not rely on them.

### Example

```luau
-- Define a component in a script
local Rotator = hype.component.define("Rotator")
function Rotator:onInit(speed: number)
    self.speed = speed or math.pi / 100
    self.entity = hype.component.getEntity(self)
end
function Rotator:onUpdate(dt: number)
    hype.transform.rotate(self.entity, hype.math.eulerToRotation(0, self.speed * dt, 0), hype.transform.Space.Local)
end

-- Spawn something and attach with an init arg
local asset = hype.asset.getById("0692d1a6a5555e560e0918")
local spawned = hype.world.spawn(asset, vector.create(128, 3, 29))
local comp = spawned:attachComponent("Rotator", math.pi/50)
```
