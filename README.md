# JSON UI Kernel

Renderer-agnostic, product-agnostic kernel contracts for declarative UI expressed as JSON.

This repository is the **strict kernel layer**, not a component library and not a product design system.

## What This Is

The kernel answers only one question:

> How is UI expressed in a stable, machine-readable, renderer-neutral form?

It defines the lowest-level contracts for:

- node composition
- binding expressions
- condition trees
- action intents
- theme references

## What This Is Not

This repository intentionally does **not** define:

- product or domain vocabulary
- token values
- component visual design
- page-level business composition
- React, Expo, Web, or PDF-specific props
- renderer implementation details

## Layer Boundary

```text
json-ui-kernel
  ↓
ui-foundation
  ↓
ui-domain-*
  ↓
app-*
  ↓
ui-renderer-*
```

The kernel sits below foundation, domain packs, apps, and renderers.

## Repository Layout

```text
schemas/
  node.schema.json
  binding.schema.json
  condition.schema.json
  action.schema.json
  theme-ref.schema.json

docs/
  ui-kernel-architecture-v1.md
  schema-taxonomy-v1.md
  core-schema-sketches-v1.md
```

## Core Contracts

### Node

Defines the normalized UI composition unit.

```json
{
  "id": "page.project-overview.root",
  "kind": "component",
  "component": "surface.card",
  "props": {},
  "slots": {},
  "bind": {},
  "visibleWhen": null,
  "actions": []
}
```

### Binding

Maps UI fields to a stable view-model namespace.

```json
{
  "text": "$data.project.name",
  "items": "$data.requirements",
  "status": "$derived.status"
}
```

### Condition

Describes visibility and branch logic without leaking renderer logic.

```json
{
  "all": [
    { "path": "$data.run.status", "op": "=", "value": "failed" },
    { "path": "$viewer.mode", "op": "!=", "value": "compact" }
  ]
}
```

### Action

Defines intent, not implementation.

```json
{
  "type": "navigate",
  "target": "page.task-detail",
  "params": {
    "taskId": "$data.task.id"
  }
}
```

### ThemeRef

Points to themes without embedding token values.

```json
{
  "theme": "foundation.dark",
  "domainTheme": "openbit.dark"
}
```

## Design Rules

- stable ids over renderer-specific names
- declarative schema over ad hoc component props
- forward-only dependency direction
- domain semantics must live above the kernel
- renderers consume kernel contracts; they do not redefine them

## Who Should Use This

This repository is suitable if you are building:

- a JSON-first UI system
- a renderer-neutral composition model
- multiple render targets from one source of truth
- a product-agnostic UI expression layer

It is **not** sufficient by itself to build an application UI. You will still need:

- a foundation system
- tokens
- a catalog
- presets
- application pages and data mapping
- one or more renderers

## Adjacent Open Source Candidates

These are good neighbors to open source separately rather than mixing into the kernel:

1. **ui-foundation**
   - generic token schemas
   - generic catalog contracts
   - generic, product-agnostic presets
2. **renderer adapter contracts**
   - schema-to-target mapping docs
   - token resolution contracts
3. **design preview pipeline**
   - static HTML / PNG / PDF preview generator
   - public design-pack publishing workflow

Keep these separate from the strict kernel to preserve boundary clarity.

## Status

This repository currently contains the v1 kernel schemas extracted from the OpenBit architecture work.

## License

No license file has been attached yet. Choose one explicitly before treating this repository as a contribution-ready open source project.
