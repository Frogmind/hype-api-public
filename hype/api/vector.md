# Vector
## Summary
Luau vector library

## Details
The `vector` library provides functions for creating and manipulating vectors. Vectors are by default 4-component (x, y, z, w),
but can be used as 3-component vectors by ignoring the w component.
Here is the type definition for the vector library:
```luau
declare vector: {
	create: (x: number, y: number, z: number?, w: number?) -> vector,
	magnitude: (vec: vector) -> number,
	normalize: (vec: vector) -> vector,
	cross: (vec1: vector, vec2: vector) -> vector,
	dot: (vec1: vector, vec2: vector) -> number,
	angle: (vec1: vector, vec2: vector, axis: vector?) -> number,
	floor: (vec: vector) -> vector,
	ceil: (vec: vector) -> vector,
	abs: (vec: vector) -> vector,
	sign: (vec: vector) -> vector,
	clamp: (vec: vector, min: vector, max: vector) -> vector,
	max: (vector, ...vector) -> vector,
	min: (vector, ...vector) -> vector,
	lerp: (vec1: vector, vec2: vector, t: number) -> vector,

	zero: vector,
	one: vector,
}
```
