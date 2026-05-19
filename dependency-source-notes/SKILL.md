---
name: dependency-source-notes
description: Explore third-party dependency source code with reusable notes. Use before expensive upstream dependency investigation, when resolving exact dependency versions and enabled features, when consulting or refreshing doc/deps/<crate>/<resolved-version>.md notes, or when implementation depends on non-obvious lifecycle, ownership, threading, callback, feature-flag, platform, API, or integration behavior.
---

# Dependency Source Notes

## Core Rule

`doc/deps/` contains non-authoritative reference notes for third-party dependencies. Notes reduce repeated source exploration; they do not define workspace design decisions, implementation plans, or boundary contracts.

Store expensive dependency notes at `doc/deps/<crate>/<resolved-version>.md` unless the project explicitly declares another path.

## Before Upstream Exploration

Before broad third-party dependency exploration:

1. Determine the exact resolved version. For Cargo crates, use `Cargo.lock`.
2. Determine relevant enabled features. For Cargo crates, use workspace manifests and `cargo metadata` when needed.
3. Consult the matching `doc/deps/<crate>/<resolved-version>.md` note if it exists.
4. Search local use sites, wrappers, adapters, re-exports, and tests before opening upstream source.
5. Read upstream source only for the exact symbols, traits, macros, modules, callbacks, or lifecycle paths needed for the current task.
6. If the note is missing, stale, or insufficient, use a read-only subagent to create or refresh it, then continue from that note.

Do not summarize unused parts of a dependency just because the source is available.

## Note Content

Dependency notes must include only:

- Dependency or crate name, exact version, enabled features, and verification date.
- Why the workspace uses the dependency for the inspected task.
- Symbols, types, traits, macros, callbacks, commands, or modules actually used or inspected.
- Lifecycle, event-loop, threading, ownership, and callback invariants relevant to the workspace.
- Integration gotchas, platform constraints, and feature-flag caveats.
- Minimal upstream source entrypoints for deeper follow-up.
- Commands and files consulted to verify the note.
- Unresolved questions, if any.

Dependency notes must not include:

- Workspace design decisions owned by design docs.
- Implementation plans owned by `doc/plan.md`.
- Environment-specific facts that belong in `ENV.md`.
- Secrets, tokens, machine-local paths outside the workspace, or private operator data.
- Broad summaries of unused parts of the dependency.

## Refresh Triggers

Refresh a dependency note when:

- The resolved dependency version changes.
- Enabled features change.
- The current task needs symbols not covered by the note.
- Current upstream source, docs, or tests contradict the note.
- Local use changes enough that the prior note no longer describes the integration.

Keep notes short, high-signal, and limited to the parts of the dependency actually used by the workspace.

## Delegated Handoff

A read-only dependency-note subagent handoff must include:

- Note path created or refreshed.
- Exact version and enabled features.
- Symbols and source files examined.
- Local use sites inspected.
- Commands run.
- Findings relevant to the current task.
- Unresolved questions and risks.

