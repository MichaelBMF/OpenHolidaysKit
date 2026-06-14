# Release and Packaging

## Goal

Define how OpenHolidaysKit releases Swift, Kotlin, and shared data artifacts.

## Decisions

- Public release packaging is not part of the first MVP.
- Versioning must make the data version visible.
- Swift Package Index and Maven/Gradle publication are planned later.

## Non-Goals

- No Maven Central release in the scaffold phase.
- No automated publishing before API and data licensing are stable.

## Open Questions

- Should code and data be versioned independently?
- Should the first Kotlin package target GitHub Packages before Maven Central?

## Verify

- Release notes identify code version and data version.
- Published artifacts contain license and notice files.
