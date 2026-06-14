# OpenHolidaysKit

OpenHolidaysKit is a planned public monorepo for a portable holiday-rule engine.
It will provide a shared specification, shared data fixtures, and native
implementations for Swift and Kotlin.

## Status

This repository is in the planning and scaffold phase. The first implementation
target is a small Germany/Bavaria subset with shared golden fixtures.

## Goals

- Provide a local, offline holiday calculation engine.
- Keep Swift and Kotlin behavior semantically identical.
- Use YAML as source input and normalized data for runtime implementations.
- Maintain shared golden fixtures and parity tests.
- Keep code licensing separate from holiday data licensing.

## Non-Goals

- No public web API.
- No UI.
- No app-specific integration.
- No full `date-holidays` data import before the data license strategy is
  finalized.
- No school holiday support in the first MVP.

## Repository Layout

- `swift/` - Swift Package implementation.
- `kotlin/` - Kotlin Multiplatform implementation.
- `data/` - source data snapshots, generated data, and attribution files.
- `specs/` - project specifications for rules, schema, API, sync, licensing,
  parity, compatibility, and release packaging.
- `tests/` - shared fixtures, golden outputs, and parity data.
- `tools/` - import, sync, validation, and fixture generation tooling.

## Licensing

The engine code in this repository is intended to be licensed under MIT.

Holiday data is licensed separately. Data imported or derived from upstream
projects keeps the applicable upstream data license and attribution
requirements. See `data/LICENSE.md` and `NOTICE.md` before adding or publishing
data.

## Planning

The current project plan lives in `.planning/plan.md`.
