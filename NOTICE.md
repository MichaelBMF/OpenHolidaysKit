# Notices

OpenHolidaysKit keeps engine code and holiday data under separate licensing
rules.

## Project Code

Original source code created for OpenHolidaysKit is licensed under MIT. See
`LICENSE`.

## Holiday Data

Holiday data may come from multiple sources. Each imported source must be
documented with:

- upstream project or publisher
- upstream URL
- upstream commit, release, or publication date
- source license
- sync/import date
- transformation tool version or commit

## date-holidays

The project may use `commenthol/date-holidays` as a data and behavior reference.
Its implementation code is ISC licensed. Its holiday YAML data has separate
data licensing and attribution requirements. Imported YAML snapshots and data
derived from them must not be relicensed as MIT.

The exact upstream commit and license copy must be stored under
`data/sources/date-holidays/` for every imported snapshot.
