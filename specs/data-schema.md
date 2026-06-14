# Data Schema

## Goal

Define the YAML input, intermediate representation, and generated data schema.

## Decisions

- YAML is the source input format.
- Runtime implementations use normalized data structures.
- Generated data must be deterministic and reproducible.

## Non-Goals

- No optimized binary data format in V1.
- No manual editing of generated data.

## Open Questions

- Should V1 parse YAML at runtime or only use generated JSON fixtures?
- Which schema validator should be used for shared validation?

## Verify

- Invalid schema input fails validation.
- Generated output is stable across repeated runs.
