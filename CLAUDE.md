# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Language

All code, code comments, commit messages, pull request titles/descriptions, documentation files,
package metadata, and release notes **must be written in English**. This applies regardless of the
language used when chatting with the user (conversation may be German).

## Project Overview

OpenHolidaysKit is a public monorepo for a portable holiday-rule engine with shared data,
specifications, and golden tests.

The repository is planned to contain:

- **Swift Package**: `OpenHolidaysKit`
- **Kotlin Multiplatform library**: `OpenHolidaysKotlin`
- **Shared specifications**: rule language, data schema, API contract, parity tests
- **Shared data pipeline**: YAML snapshots, normalized generated data, attribution files
- **Golden fixtures**: the source of truth for Swift/Kotlin parity

The project is intentionally standalone. It must not depend on the Time Tracking Calendar app.
Consumers can later add their own adapters.

## Current Development Phase

Start with the project plan in [.planning/plan.md](.planning/plan.md).

Initial goal:

1. Scaffold the monorepo structure.
2. Establish licensing and data-boundary documentation.
3. Add skeleton specifications.
4. Add the `date-holidays` YAML sync workflow design.
5. Build the first Swift/Kotlin MVP against shared golden fixtures.

## Licensing Model

Keep code and data licensing separate.

- Own source code: MIT.
- Own minimal fixtures: MIT or CC0, decided in `data/LICENSE.md`.
- `date-holidays` YAML snapshots: keep the upstream data license and attribution.
- Generated data derived from `date-holidays` YAML must be treated as derived data, not
  re-licensed as MIT.

Do not copy upstream implementation code unless the license and attribution impact are explicitly
handled. Prefer reimplementing behavior from the written specs and validating with fixtures.

## Architecture

The shared source of truth is:

1. Specifications in `specs/`
2. Source YAML snapshots in `data/sources/`
3. Normalized generated data in `data/generated/`
4. Golden fixtures in `tests/golden/`

Swift and Kotlin implementations must implement the same specs and pass the same fixtures. Neither
implementation should become the implicit reference for the other.

Planned top-level structure:

- `.github/workflows/` — CI and data-sync workflows
- `data/` — source snapshots, generated data, licenses, attribution
- `specs/` — rule language, data schema, API contract, parity, release docs
- `swift/` — Swift Package
- `kotlin/` — Kotlin Multiplatform project
- `tests/` — shared fixtures, golden outputs, parity assets
- `tools/` — sync, validation, import, and fixture-generation tools

## Data Sync

`date-holidays` data should be consumed as a reproducible snapshot, not by making this repository a
GitHub fork and deleting unrelated code.

The sync workflow should:

- checkout `commenthol/date-holidays` at an explicit ref
- copy the YAML data unchanged into `data/sources/date-holidays/countries/`
- copy the upstream license into `data/sources/date-holidays/LICENSE`
- write `data/sources/date-holidays/UPSTREAM.md` with repo, commit, sync date, tool version, and
  license notes
- generate normalized data into `data/generated/`
- validate data and fixtures
- open a pull request instead of committing directly to `main`

## Testing Strategy

Tests are the core quality gate.

Required layers:

- Unit tests for date/rule calculations.
- Parser tests for YAML and normalized IR.
- Golden tests for country/year/profile outputs.
- Parity tests so Swift and Kotlin produce equivalent results.
- Optional reference checks against `date-holidays` JS for defined fixture sets.

Every rule feature should arrive with a fixture before broad data import expands its use.

## Behavioral Guidelines

Behavioral guidelines to reduce common LLM coding mistakes. Merge with project-specific
instructions as needed.

**Tradeoff:** These guidelines bias toward caution over speed. For trivial tasks, use judgment.

## 1. Think Before Coding

**Don't assume. Don't hide confusion. Surface tradeoffs.**

Before implementing:

- State your assumptions explicitly. If uncertain, ask.
- If multiple interpretations exist, present them; don't pick silently.
- If a simpler approach exists, say so. Push back when warranted.
- If something is unclear, stop. Name what's confusing. Ask.

## 2. Simplicity First

**Minimum code that solves the problem. Nothing speculative.**

- No features beyond what was asked.
- No abstractions for single-use code.
- No flexibility or configurability that was not requested.
- No error handling for impossible scenarios.
- If you write 200 lines and it could be 50, rewrite it.

Ask yourself: "Would a senior engineer say this is overcomplicated?" If yes, simplify.

## 3. Surgical Changes

**Touch only what you must. Clean up only your own mess.**

When editing existing code:

- Don't improve adjacent code, comments, or formatting unless it is necessary for the task.
- Don't refactor things that are not broken.
- Match existing style, even if you would do it differently.
- If you notice unrelated dead code, mention it; don't delete it.

When your changes create orphans:

- Remove imports/variables/functions that your changes made unused.
- Don't remove pre-existing dead code unless asked.

The test: Every changed line should trace directly to the user's request.

## 4. Goal-Driven Execution

**Define success criteria. Loop until verified.**

Transform tasks into verifiable goals:

- "Add validation" -> "Write tests for invalid inputs, then make them pass"
- "Fix the bug" -> "Write a test that reproduces it, then make it pass"
- "Refactor X" -> "Ensure tests pass before and after"

For multi-step tasks, state a brief plan:

```text
1. [Step] -> verify: [check]
2. [Step] -> verify: [check]
3. [Step] -> verify: [check]
```

Strong success criteria let you loop independently. Weak criteria ("make it work") require
clarification.

## Git & GitHub Workflow

- Use feature branches for all changes.
- Keep pull requests small and reviewable.
- Use English commit messages and PR descriptions.
- For data-sync workflows, create PRs rather than pushing generated changes directly to `main`.
- When merging PRs with the `gh` CLI, use `gh pr merge --delete-branch` to delete the source branch
  after merge.
