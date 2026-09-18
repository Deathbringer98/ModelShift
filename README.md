# ModelShift

**A vendor neutral developer method for safely handing off software projects between AI coding models and agents while preserving context, engineering quality, and development velocity.**

## What is ModelShift?

**ModelShift** is a cross model AI development methodology designed to make switching between AI coding agents predictable and reliable.

Before transferring work, the outgoing agent stabilizes the repository, verifies builds and tests, records its current state, decisions, unfinished work, and next actions, then creates a structured handoff for the incoming agent.

The incoming agent independently validates that handoff against the repository, Git history, builds, and tests before continuing development.

ModelShift treats AI agents as interchangeable engineering collaborators while treating **the repository, version control, documentation, and reproducible verification as the persistent source of truth.**

## Core Principle

> **Stop → Verify → Checkpoint → Handoff → Validate → Continue**

The goal of ModelShift is simple:

**Maintain solid engineering while minimizing the time and friction required to move development between different AI models, vendors, sessions, or specialized agents.**

## Why ModelShift?

AI coding agents can produce substantial amounts of software quickly, but development can be interrupted by usage limits, context limits, cost, model availability, or simply because another model is better suited to the next task.

Switching models without a proper handoff can result in:

* Lost development context
* Duplicate work
* Architecture drift
* Conflicting implementations
* Unfinished refactors
* Incorrect assumptions
* Previously fixed bugs returning
* Tests or build failures being overlooked

ModelShift provides a simple process for transferring that work without requiring the next model to reconstruct the previous session.

## Basic Workflow

```text
Developer
    │
    ▼
Model A
    │
    ▼
Stop
    │
Verify
    │
Checkpoint
    │
Handoff
    │
    ▼
Model B
    │
Validate
    │
Continue
    ▼
Development
```

The outgoing agent should leave behind a clear `AGENT_HANDOFF.md` containing the current state of development. Start from [`AGENT_HANDOFF_TEMPLATE.md`](AGENT_HANDOFF_TEMPLATE.md).

The incoming agent reads the handoff, inspects the repository, verifies the build and tests, and only then continues development.

## Example Handoff

```markdown
# Agent Handoff

Current branch / commit:

Current objective:

Completed:

Partially completed:

Remaining TODOs:

Files modified:

Architecture decisions:

Important assumptions:

Known bugs:

Build command:

Test command:

Latest build result:

Latest test result:

Recommended first action:
```

## Cross Model Development

ModelShift is vendor neutral.

A development workflow could move between any combination of coding agents:

```text
Model A
   ↓
ModelShift
   ↓
Model B
   ↓
ModelShift
   ↓
Model C
   ↓
ModelShift
   ↓
Model A
```

The specific AI provider is not important.

The repository remains the persistent source of truth while individual models can be changed whenever necessary.

## Verification Matters

A handoff is not automatically trustworthy simply because another AI produced it.

If the outgoing model reports that all tests pass, the incoming model should independently run those tests.

The priority should be:

```text
Repository
    ↓
Git History
    ↓
Build Results
    ↓
Tests
    ↓
Documentation
    ↓
Agent Handoff
```

The handoff provides context.

**The repository provides evidence.**

## Parallel Agents

ModelShift can also be combined with Git branches or worktrees when multiple agents are working simultaneously.

```text
                 Main
                  │
        ┌─────────┼─────────┐
        ▼         ▼         ▼
     Agent A   Agent B   Agent C
      Engine      UI       Tests
        │         │         │
        └─────────┼─────────┘
                  ▼
              Review / CI
                  │
                  ▼
                 Main
```

Agents working in parallel should generally be isolated from one another rather than modifying the same working tree.

## Specialized Agents

ModelShift can also be used to transfer work between agents with different responsibilities.

```text
Implementation Agent
        ↓
    ModelShift
        ↓
Review Agent
        ↓
    ModelShift
        ↓
Testing Agent
        ↓
    ModelShift
        ↓
Human Review
```

Possible roles include:

* Architecture
* Implementation
* Testing
* Security
* Performance
* Documentation
* Refactoring
* Code review

## Experiment With It

ModelShift is intended to be adapted.

Developers can experiment with:

* Different handoff formats
* Different AI providers
* Model rotation
* Independent model reviews
* Specialized agent roles
* Git worktrees
* Automated handoff generation
* Automated verification
* CI integration
* Context loss testing

One useful experiment is starting a completely fresh AI session with nothing except the repository and ModelShift documentation.

If the new agent can verify the project and continue development correctly, the project has strong context portability.

## Recommended Repository Structure

```text
project/
├── AGENTS.md
├── AGENT_HANDOFF.md
├── README.md
├── docs/
├── src/
└── tests/
```

`AGENTS.md` contains persistent project rules and engineering requirements.

`AGENT_HANDOFF.md` contains temporary development state for the next agent.

Git records what actually changed.

Tests provide reproducible verification.

## Philosophy

ModelShift is based on a simple idea:

> **AI models should not be the permanent holders of project knowledge.**

Models can change.

Providers can change.

Sessions can end.

Context can disappear.

The project should remain understandable and recoverable regardless of which model worked on it previously.

**Models are interchangeable collaborators. The repository is the persistent engineering record.**

## Documentation

A more detailed explanation of the methodology, example workflows, suggested handoff procedures, and areas for experimentation is available in:

**[`docs/ModelShift_Method.pdf`](docs/ModelShift_Method.pdf)**

## Repository Contents

```text
ModelShift/
├── README.md
├── LICENSE
├── AGENTS.md
├── AGENT_HANDOFF_TEMPLATE.md
└── docs/
    └── ModelShift_Method.pdf
```

* [`AGENTS.md`](AGENTS.md): example persistent rules for agents, following the ModelShift method
* [`AGENT_HANDOFF_TEMPLATE.md`](AGENT_HANDOFF_TEMPLATE.md): copy to `AGENT_HANDOFF.md` in your project and fill it in at each handoff

## Contributing

ModelShift is an experimental development methodology.

If you discover a better handoff structure, verification technique, multi model workflow, automation strategy, or other improvement, experimentation and contributions are encouraged.

Fork it. Test it. Modify it. Measure it. Improve it.

## License

Released under the [MIT License](LICENSE). Use, modify, and adapt the ModelShift methodology for your own development workflows.
