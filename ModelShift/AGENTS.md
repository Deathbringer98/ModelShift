# AGENTS.md

Persistent rules for any AI coding agent working in this repository.

This file is the stable engineering contract. Temporary development state belongs in `AGENT_HANDOFF.md` (see `AGENT_HANDOFF_TEMPLATE.md`), not here.

## Project

ModelShift is a documentation-only repository describing a vendor neutral method for handing off software development between AI coding models and agents.

| Path | Purpose |
| --- | --- |
| `README.md` | Overview of the method, workflow, and philosophy |
| `AGENTS.md` | This file: persistent rules for agents |
| `AGENT_HANDOFF_TEMPLATE.md` | Template the outgoing agent fills in as `AGENT_HANDOFF.md` |
| `docs/Cross_Model_Handoff_Developer_Method.pdf` | Full write-up of the method |
| `LICENSE` | MIT License |

## Operating Principle

**Speed is the optimization. Engineering quality is the constraint.**

> **Stop → Verify → Checkpoint → Handoff → Validate → Continue**

## Source of Truth

When sources disagree, trust them in this order:

1. Repository contents
2. Git history
3. Build results
4. Tests
5. Documentation
6. Agent handoff

The handoff provides context. The repository provides evidence.

## Before Modifying Anything (Incoming Agent)

1. Read `AGENTS.md`, the project documentation, and `AGENT_HANDOFF.md` if present.
2. Inspect `git status`, recent commits, and every file referenced by the handoff.
3. Independently run the documented build and test commands.
4. If the handoff conflicts with repository reality, document the discrepancy and reconcile it before continuing.
5. Continue from the first verified incomplete task, preserving established architecture unless a change is explicitly justified.

## Before Stopping (Outgoing Agent)

1. Stop starting new functionality before the model, credit, or context limit is exhausted.
2. Bring the repository to the safest practical checkpoint. Do not leave unexplained half-edits.
3. Inspect `git status` and summarize all modifications.
4. Run the relevant build and test commands. Record exact failures and suspected causes.
5. Create a coherent commit, or clearly document uncommitted work.
6. Copy `AGENT_HANDOFF_TEMPLATE.md` to `AGENT_HANDOFF.md` and fill it in.
7. Do not begin the next feature after completing the handoff.

## Rules

* Keep handoffs factual and short enough to be read.
* Record exact commands and results instead of saying "tests work."
* Never manufacture a green checkpoint by disabling or skipping tests.
* Prefer small, coherent commits.
* Make failures visible.
* Keep permanent architecture decisions in durable documentation, not the temporary handoff.
* Verify rather than blindly trust a previous agent's claims.
* Parallel agents must work in separate branches or worktrees, never the same working tree.

## Definition of Done

A task is not complete because an agent says it is complete. Completion is demonstrated by evidence appropriate to the project: successful builds, automated tests, static analysis, benchmarks, integration checks, reproducible packaging, or manual acceptance criteria.

## Repository-Specific Notes

* This repository has no build or test step. Verification means checking that links and file paths referenced in the documentation exist and that Markdown renders correctly.
* Keep the method vendor neutral. Do not favor a specific AI provider in the documentation.
