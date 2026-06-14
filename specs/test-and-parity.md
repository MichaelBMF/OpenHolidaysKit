# Test and Parity

## Goal

Define how behavior is verified across rule logic, parsers, fixtures, Swift, and
Kotlin.

## Decisions

- Shared golden fixtures are the compatibility baseline.
- Swift and Kotlin tests must consume the same fixtures.
- Optional reference tests may compare against `date-holidays` JavaScript.

## Non-Goals

- Reference tests do not make the JS implementation a runtime dependency.
- Parity tests do not replace unit tests for individual rule types.

## Open Questions

- Which countries beyond Germany/Bavaria should be first parity targets?
- Should reference tests run in CI by default or only manually?

## Verify

- Intentionally changing a known holiday date fails parity validation.
- Unsupported rules are visible in test reports.
