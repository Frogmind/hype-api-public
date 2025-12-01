# Math

## API Reference

## lerp

Linearly interpolates between two vectors.

### Signature

```luau
hype.math.lerp(start: vector, end: vector, t: number): vector
```

### Parameters
- t - interpolation factor (not clamped)

### Notes
- t=0 returns start; t=1 returns end; values outside [0,1] extrapolate

## snapToGrid

Snaps a vector to a per-axis grid.

### Signature

```luau
hype.math.snapToGrid(v: vector, grid: vector): vector
```

### Parameters
- v - input value
- grid - grid cell size per axis

### Notes
- Each axis is snapped to nearest multiple of grid component when > 0; if grid component <= 0, that axis is left unchanged

## rotateVector

Rotates a vector by a rotation.

### Signature

```luau
hype.math.rotateVector(v: vector, r: rotation): vector
```

### Parameters
- v - vector to rotate
- r - rotation (quaternion)

### Notes
- The rotation should be normalized; result is the rotated vector in the same space

## splinePosition

Position along a spline segment defined by 4 points.

### Signature

```luau
hype.math.splinePosition(t: number, tension0: number, tension1: number, p0: vector, p1: vector, p2: vector, p3: vector): vector
```

### Parameters
- t - relative distance along segment [0,1]
- tension0 - start tension parameter
- tension1 - end tension parameter
- p0 - previous control point
- p1 - segment start point
- p2 - segment end point
- p3 - next control point

### Notes
- Returns the interpolated position on the spline between p1 and p2

## splineTangent

Tangent (derivative) of the spline at relative distance t.

### Signature

```luau
hype.math.splineTangent(t: number, tension0: number, tension1: number, p0: vector, p1: vector, p2: vector, p3: vector): vector
```

### Parameters
- t - relative distance along segment [0,1]
- tension0 - start tension parameter
- tension1 - end tension parameter
- p0 - previous control point
- p1 - segment start point
- p2 - segment end point
- p3 - next control point

### Notes
- Returns the tangent/derivative vector; it may not be unit length

## splineLength

Estimated arc length of the spline segment between p1 and p2.

### Signature

```luau
hype.math.splineLength(tension0: number, tension1: number, p0: vector, p1: vector, p2: vector, p3: vector): number
```

### Parameters
- tension0 - start tension parameter
- tension1 - end tension parameter
- p0 - previous control point
- p1 - segment start point
- p2 - segment end point
- p3 - next control point

## distance

Euclidean distance between two points.

### Signature

```luau
hype.math.distance(a: vector, b: vector): number
```

### Parameters
- a - first point
- b - second point

## distanceSqr

Squared distance between two points (no sqrt).

### Signature

```luau
hype.math.distanceSqr(a: vector, b: vector): number
```

### Parameters
- a - first point
- b - second point

### Notes
- Useful for comparisons without the cost of square root

## eulerToRotation

Converts Euler angles to a rotation (quaternion).

### Signature

```luau
hype.math.eulerToRotation(euler: vector): rotation
```

### Parameters
- euler - Euler angles in radians; can be provided as a vector or separate components

### Notes
- Expects radians; use math.rad/deg conversion as needed

## slerp

Spherical linear interpolation between two rotations.

### Signature

```luau
hype.math.slerp(a: rotation, b: rotation, t: number): rotation
```

### Parameters
- a - start rotation (quaternion)
- b - end rotation (quaternion)
- t - interpolation factor in [0,1]

### Notes
- t outside [0,1] extrapolates along the shortest arc

## directionToRotation

Rotation that orients the forward axis to the given direction.

### Signature

```luau
hype.math.directionToRotation(dir: vector): rotation
```

### Parameters
- dir - target direction; zero-length is invalid

### Notes
- Uses global up (0,1,0) as the up vector
- The direction is normalized internally

## lookAt

Look-at rotation from a position toward a target.

### Signature

```luau
hype.math.lookAt(pos: vector, target: vector): rotation
```

### Parameters
- pos - source position
- target - point to look at

### Notes
- Uses global up (0,1,0) as the up vector
- If pos == target the result is undefined

## toEuler

Converts a rotation (quaternion) to Euler angles.

### Signature

```luau
hype.math.toEuler(r: rotation): vector
```

### Parameters
- r - input rotation (quaternion)

### Notes
- Returns Euler angles in radians

## axisAngle

Creates a rotation from an angle and axis.

### Signature

```luau
hype.math.axisAngle(angle: number, axis: vector): rotation
```

### Parameters
- angle - rotation angle in radians
- axis - rotation axis; should be unit length

## dirAndUpToRot

Rotation that orients the forward axis to dir with a given up vector.

### Signature

```luau
hype.math.dirAndUpToRot(dir: vector, up: vector): rotation
```

### Parameters
- dir - forward direction; zero-length is invalid
- up - up direction; should not be colinear with dir

### Notes
- Both vectors are normalized internally
