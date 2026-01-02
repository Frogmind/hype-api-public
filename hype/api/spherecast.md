# sphereCast

## sphereCast

Casts a sphere along a ray and returns hit records (or an empty table if no hit).

### Signature

```luau
hype.physics.sphereCast(origin: vector, ray: vector, radius: number, extraParams: { groupFilter: {number}?, ignoreGroupFilter: {number}?, ignoredEntities: {Entity}? }?): { { entity: Entity?, position: vector, normal: vector }? }
```

### Parameters
- origin - start position (world space)
- ray - direction * length; length is |ray|; ignored if near zero
- radius - sphere radius (> 0)
- extraParams - optional parameters
  - extraParams.groupFilter - groups to include (whitelist)
  - extraParams.ignoreGroupFilter - groups to exclude (blacklist)
  - extraParams.ignoredEntities - entities to skip

### Notes
- Returns an empty table when no hit occurs, ray length is zero, or radius <= 0
- Returned normal is unit length; position is world space
