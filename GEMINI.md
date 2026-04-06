# Spec-Driven Development (SDD) Workflow

This extension enables a Spec-Driven Development (SDD) workflow within Gemini CLI. This process prioritizes clear specifications and rigorous validation to ensure that all changes align with user requirements.

## Core Mandates

### 1. Specification First
- **Structure & Location:** Every project MUST maintain its specification in the `./docs/specification` folder. 
- **Persistent Specification:** `requirements.md`, `design.md`, and `test-strategy.md` are the source of truth and must be updated with every change.
- **Transactional Tasks:** Every story/epic must have a `tasks.md` in a `[seq]-[slug]` folder.
- **Validation:** Always verify requirements, design, and test strategy before starting implementation.

### 2. Architect Mode (Assertive & Detailed)
When operating in SDD, you MUST adopt "Architect Mode." This means:
- **Explicit Verbosity:** Never summarize. Provide exhaustive detail in every artifact. Include full API schemas, comprehensive data models, and every possible error-handling state for every component.
- **Precision over Brevity:** Use formal technical language and avoid vague marketing speak.
- **Traceability:** Every single decision must be traceable back to a requirement or an ADR.

### 3. Chain-of-Thought (Architectural Reasoning)
Before drafting or updating any SDD artifact, you MUST perform an internal "Step-by-Step Architectural Audit":
1. **Analyze Constraints:** What are the hard limits of the current environment?
2. **Evaluate Trade-offs:** What are the pros and cons of the proposed approach vs. alternatives?
3. **Trace Dependencies:** What existing components or services will this change impact?
4. **Predict Failures:** What are the edge cases and failure modes for this specific logic?

## SDD Lifecycle
The SDD workflow follows a strict sequence:
1. **Init:** Establish the structure (`/sdd:init`).
2. **Requirements:** Define the scope (`/sdd:requirements`).
3. **Design:** Plan the solution and verification (`/sdd:design`).
4. **Tasking:** Create the execution plan (`/sdd:tasks`).
5. **Execution:** Implement the solution story-by-story (`/sdd:execute`).
6. **Validation:** Ensure final compliance with the spec (`/sdd:check`).

## Development Standards

### 1. Commit Conventions
All commits MUST follow the [Conventional Commits](https://www.conventionalcommits.org/) specification. This is enforced via `commitlint` and `husky` and is used to automate versioning and releases.
- **feat:** A new feature (corresponds to a MINOR version bump).
- **fix:** A bug fix (corresponds to a PATCH version bump).
- **chore/docs/style/refactor/test:** Maintenance tasks that do NOT trigger a new release.
- **BREAKING CHANGE:** Use `!` or `BREAKING CHANGE:` in the footer for a MAJOR version bump.

## SDD Skill & Commands

For detailed guidance and automated workflows, activate the **SDD Skill**:
`activate_skill("sdd")`

### Available Commands:
- `/sdd:init`: Initialize the SDD specification structure and inspect existing code.
- `/sdd:requirements`: Define or update functional and non-functional requirements.
- `/sdd:design`: Define or update implementation strategy and BDD-style test scenarios.
- `/sdd:tasks`: Create a transactional tasks.md file for a specific story or epic.
- `/sdd:execute`: Implement a user story, adhering to design and local standards.
- `/sdd:check`: Analyze compliance with SDD mandates and the specification structure.

Refer to the **SDD Skill** (`skills/sdd/SKILL.md`) for complete workflow diagrams and implementation guidelines.
