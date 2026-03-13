# `ui-kernel` Schemas

These schemas are the first machine-readable implementation of the v1 kernel contracts documented in:

- `design/ui-system/ui-kernel-architecture-v1.md`
- `design/ui-system/schema-taxonomy-v1.md`
- `design/ui-system/core-schema-sketches-v1.md`

## Files

- `node.schema.json`
  - renderable node contract
- `binding.schema.json`
  - declarative binding map and recursive binding values
- `condition.schema.json`
  - declarative visibility and branch logic
- `action.schema.json`
  - renderer-agnostic action contract
- `theme-ref.schema.json`
  - symbolic theme references

## Notes

- Draft target: JSON Schema 2020-12
- These schemas intentionally stay conservative for v1
- Renderer-specific concerns must remain outside this directory
