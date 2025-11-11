# Camera
## Summary
Camera controls for the active world.

## API Reference

## getPosition

Returns current camera world position.

### Signature

```luau
hype.camera.getPosition(): vector
```

### Returns
A Vector3 (x, y, z).

## getDirection

Returns current camera forward direction (normalized).

### Signature

```luau
hype.camera.getDirection(): vector
```

### Returns
A normalized Vector3 forward direction.

## getRotation

Returns current camera rotation as a quaternion.

### Signature

```luau
hype.camera.getRotation(): vector
```

### Returns
A Vector4 quaternion (x, y, z, w).

## getFov

Returns camera vertical field of view in degrees.

### Signature

```luau
hype.camera.getFov(): number
```

### Returns
Field of view in degrees.

## setFov

Sets camera vertical field of view in degrees.

### Signature

```luau
hype.camera.setFov(fovDeg: number): ()
```

### Parameters
- fovDeg - field of view in degrees.

## getEntity

Returns the camera entity if one exists in the world.

### Signature

```luau
hype.camera.getEntity(): Entity?
```

### Returns
The camera entity, or nil if not available.
