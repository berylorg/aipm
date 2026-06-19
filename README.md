# AIPM

AIPM is a set of Codex skills for keeping AI-assisted software work aligned with product intent, system architecture, package boundaries, and durable plans.

It is for projects where local code edits are not enough. The goal is to make the important intent explicit in files, so an agent can reason from the project instead of from conversation history.

## Problems AIPM Solves

AI agents are good at small local changes. They are much weaker at preserving whole-project consistency unless the project gives them explicit authority to follow.

AIPM helps keep the codebase, documentation, and architecture aligned:

- Product features, system architecture, workspace-project boundaries, and code should not contradict each other.
- Each workspace project, such as a library, service, app, or plugin, should have a well-defined public boundary and should not leak responsibilities into its neighbors.
- System architecture should serve product features, and package-level decisions should serve the system architecture.
- Architectural intent should be explicit enough to review automatically in merge requests or CI/CD gates.
- Refactoring should be less painful because the higher-level intent survives outside the current code shape.
- Large architectural rework should not be forced through incremental compatibility changes just because that is the default AI tendency.
- Expensive investigations, failed approaches, and work in progress should be preserved so later sessions do not repeat the same cost.

## How AIPM Works

AIPM treats documentation as an authority chain.

`feature-design-docs` establishes feature specs for user-visible product behavior. Feature docs describe workflows, visible states, errors, and acceptance rules. They do not descend into technical architecture.

`system-design-docs` establishes system specs for cross-feature and cross-package architecture. System docs explain how workspace projects fit together in service of the feature docs, without owning the private implementation of each package.

`workspace-package-policy` establishes package-level specs for each workspace project. These docs define the package's public contract, non-negotiable decisions, responsibilities, and boundaries.

`project-doc-authority` keeps those layers ordered. It tells the agent where a decision belongs and forces contradictions to be resolved in the right authority layer before implementation depends on them.

The remaining skills protect the workflow around that authority chain:

- `implementation-planning` keeps active work in `doc/plan.md`, phased so each phase has no more than one hard task.
- `architectural-rework` makes heavy rework explicit, removal-first, and resistant to accidental compatibility layers.
- `exploration-memory` caches third-party source, documentation, paper, and research investigations under `doc/memory/`.
- `failure-logging` records invalidated design or coding approaches under `doc/failures/`.
- `subagent-orchestration` lets the main agent delegate broad exploration or review while keeping ownership of decisions and integration.

## Real Workflows

### New Feature Without Architectural Rework

1. Design the feature with the AI.
2. Ask the AI to update the architecture. This usually means system design docs and affected package docs.
3. Review the docs.
4. Ask the AI to plan the implementation in `doc/plan.md`.
5. Ask the AI to start implementation.

By default, AIPM-style work stops after each planned phase for review, thread compaction, or both. Automated compaction between phases needs agent support; [Beryl](https://github.com/berylorg/beryl/) supports this model, though it is not 1.0 yet.

### Architectural Rework

1. Define what is being replaced.
2. Ask the AI to plan the rework.
3. Review `doc/rework/<name>/REWORK.md` and the target docs it points to.
4. Ask the AI to plan implementation in `doc/plan.md`.
5. Ask the AI to start implementation.

The rework skill pushes the agent away from quietly adapting old code. Obsolete docs and source are archived, target-state docs stay authoritative, and incomplete cutover gaps remain visible.

### Onboarding An Existing Project

1. Install the skills into `<project_repo>/.agents/skills/`.
2. Ask the AI to reverse-engineer the codebase into feature, system, and workspace-project docs.
3. Review and clean up the generated docs.

The generated structure is usually close, but `Non-goals` often need human cleanup because they encode product and architecture judgment.

## License

Apache License 2.0. See [`LICENSE`](LICENSE).
