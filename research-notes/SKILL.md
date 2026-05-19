---
name: research-notes
description: Research and log external evidence for project work. Use when academic papers, standards, official documentation, source repositories, benchmarks, algorithms, UX evidence, legal or regulatory references, or other external sources inform design, planning, implementation, or review; preserve doc/research.md logging for each researched paper or source.
---

# Research Notes

## Core Rule

Lean on academic papers for non-trivial tasks. Use primary sources for technical facts whenever possible.

Log each researched paper or source in `doc/research.md` unless the project explicitly declares another research log. Research notes support reasoning and do not override design authority. Accepted target-state decisions must move into the controlling design docs.

## Source Selection

Prefer:

- Academic papers for non-trivial algorithms, evaluation methods, human factors, distributed systems, security, performance, machine learning, or complex product-behavior claims.
- Official documentation, standards, specifications, RFCs, source repositories, and release notes for APIs, tools, file formats, protocols, and dependency behavior.
- Primary project or vendor sources for current behavior.
- Reputable secondary sources only when primary sources are unavailable or when comparison is useful.

For unstable or current facts, verify with up-to-date sources.

## Research Workflow

1. State the question the research must answer.
2. Identify the evidence needed.
3. Search or inspect sources narrowly.
4. Record the source identity: title, authors or owner, URL or local path, version, date, and access date when relevant.
5. Summarize why the source was researched.
6. Summarize what was useful, or why it was not useful.
7. Explain how the finding affects design, plan, implementation, or review.
8. Update authoritative docs if the research changes target state.

Do not paste long copyrighted excerpts. Prefer paraphrase and short exact quotes only when wording matters.

## `doc/research.md` Entry Content

Each entry should include:

- Paper or source.
- Research question or reason for reading it.
- Relevant finding.
- Outcome: useful, not useful, inconclusive, or background only.
- Design, plan, implementation, or test impact.
- Follow-up questions or risks.

Keep entries short and high signal. Avoid broad literature dumps.

## Interaction With Failure Logs

If research invalidates a planned or implemented approach in a way future agents should remember, also use the failure-logging workflow.

