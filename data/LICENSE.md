# Data Licensing

OpenHolidaysKit separates engine code from holiday data.

## Own Fixtures

Small handcrafted fixtures created specifically for this project may be released
under MIT or CC0. The chosen license must be stated next to the fixture set.

## Imported Data

Imported data keeps the applicable upstream license. Do not copy imported data
into MIT-licensed files unless the upstream license explicitly allows that.

## date-holidays Data

YAML snapshots imported from `commenthol/date-holidays` and data generated from
those snapshots are treated as derived data. They must keep attribution and the
applicable upstream data license.

Every snapshot must include:

- `data/sources/date-holidays/UPSTREAM.md`
- `data/sources/date-holidays/LICENSE`
- attribution notes under `data/attributions/`
