# API Contract

## Goal

Define the shared semantic API contract for Swift and Kotlin.

## Decisions

- Holidays are local dates without time or timezone.
- Unknown data is represented as explicit status, not a silent empty result.
- Swift and Kotlin return equivalent sorted output for equivalent input.
- Localized names use a defined fallback order.

## Non-Goals

- No network API.
- No UI-specific models.
- No application-specific adapter API.

## Open Questions

- Should the first API expose raw rule metadata?
- How should provider-specific holiday types be represented?

## Verify

- Swift and Kotlin golden fixture outputs match byte-for-byte after normalization.
- Missing localization falls back deterministically.
