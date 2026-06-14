# License and Data

## Goal

Define how OpenHolidaysKit separates engine code licensing from holiday data
licensing.

## Decisions

- Original engine code is MIT licensed.
- Data licensing is documented separately in `data/LICENSE.md`.
- Imported data keeps upstream license and attribution requirements.
- Data derived from imported snapshots is treated as derived data, not MIT code.

## Non-Goals

- This spec does not approve importing the full `date-holidays` data set.
- This spec does not replace legal review for public data releases.

## Open Questions

- Should derived `date-holidays` data be published as a separate data package?
- Should handcrafted fixtures be MIT or CC0?

## Verify

- `LICENSE` covers only original project code.
- `NOTICE.md` and `data/LICENSE.md` describe data licensing boundaries.
