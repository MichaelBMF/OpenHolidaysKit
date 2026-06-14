# date-holidays Sync

## Goal

Define a reproducible process for importing YAML snapshots from
`commenthol/date-holidays`.

## Decisions

- Snapshots are copied into `data/sources/date-holidays/`.
- `UPSTREAM.md` records the exact upstream source.
- Sync workflows create pull requests instead of committing directly to `main`.
- Unsupported rules must be reported explicitly.

## Non-Goals

- No automatic full-country support in the first MVP.
- No runtime dependency on the JavaScript implementation.

## Open Questions

- Should scheduled sync be enabled from the first public commit?
- Which upstream ref should be used for the first snapshot?

## Verify

- Sync output is deterministic.
- Upstream commit, license, and attribution are recorded.
- Unsupported rules produce a machine-readable report.
