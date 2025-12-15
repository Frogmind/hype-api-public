# Voxels
## Summary
Access to voxel map editing helpers.

## Details
The `hype.voxels` namespace exposes functions for querying and mutating the voxel grid that
is attached to the current world. All coordinates refer to voxel coordinates inside the active
map (origin at the minimum corner unless otherwise specified).

## API Reference

## isActive

Returns whether a voxel map is currently active.

### Signature

```luau
hype.voxels.isActive(): boolean
```

### Returns
`true`  if the world contains a voxel map. `false` otherwise.

## getDimensions

Returns voxel grid dimensions as `{ x, y, z }`.

### Signature

```luau
hype.voxels.getDimensions(): vector?
```

### Returns
nil when no voxel map is active.

## getMaterialAt

Gets the material id stored at the given voxel coordinate.

### Signature

```luau
hype.voxels.getMaterialAt(index: vector): number?
```

### Parameters
- index - voxel coordinates `{ x, y, z }`

### Returns
Material id or nil when the voxel is empty/out of bounds/not active.

## setMaterialAt

Sets the material id stored at a voxel.

### Signature

```luau
hype.voxels.setMaterialAt(index: vector, materialId: number): ()
```

### Parameters
- index - voxel coordinates `{ x, y, z }`
- materialId - material index in the voxel world.

## isGroundAt

Checks whether a solid voxel exists at the given coordinate.

### Signature

```luau
hype.voxels.isGroundAt(index: vector): boolean?
```

### Returns
`true` when the voxel is present, `false` when empty, or nil if out of bounds/not active.

## removeAt

Removes the voxel at the given coordinate.

### Signature

```luau
hype.voxels.removeAt(index: vector): ()
```

## worldToVoxel

Converts a world position into voxel coordinates.

### Signature

```luau
hype.voxels.worldToVoxel(worldPos: vector): vector?
```

### Returns
Voxel coordinates `{ x, y, z }`, or nil if the point lies outside the voxel bounds.

## voxelToWorld

Converts voxel coordinates to a world-space position.

### Signature

```luau
hype.voxels.voxelToWorld(index: vector): vector?
```

### Returns
World position of the voxel cell center, or nil when no voxel map is active.

## raycast

Casts a ray against the voxel grid.

### Signature

```luau
hype.voxels.raycast(origin: vector, direction: vector, maxDistance: number): { distance: number, position: vector, normal: vector }?
```

### Returns
nil if the ray misses or when no voxel map is active.
