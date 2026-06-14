# Compatibility

## Goal

Define supported language and platform versions.

## Decisions

- Compatibility must be explicit before the first implementation release.
- Swift and Kotlin target matrices must be documented in this spec.
- Platform compatibility should be tested in CI where practical.

## Non-Goals

- No broad legacy platform support by default.
- No app-specific deployment target decisions in this project.

## Open Questions

- Minimum Swift version?
- Minimum macOS and iOS versions for the Swift package?
- Minimum Kotlin version?
- Minimum JVM and Android API levels?

## Verify

- CI runs on the documented toolchain versions.
- README links to the supported compatibility matrix.
