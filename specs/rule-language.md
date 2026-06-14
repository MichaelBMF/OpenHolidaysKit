# Rule Language

## Goal

Specify the holiday rule language implemented by both Swift and Kotlin.

## Decisions

V1 supports:

- fixed Gregorian dates
- Easter-relative dates
- weekday-in-month rules
- region conditions
- validity intervals
- type and localized-name metadata

## Non-Goals

- No non-Gregorian calendar support in V1.
- No astronomical rules in V1.
- No government-announced ad-hoc holidays in V1.

## Open Questions

- How closely should the rule language mirror `date-holidays` syntax?
- Which observed/substitute-day rules belong in V1?

## Verify

- Bavaria 2026 and 2030 can be represented fully.
- Unsupported upstream rules produce structured reports.
