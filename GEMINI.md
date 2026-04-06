# Spec-Driven Development (SDD) Workflow

This extension enables a Spec-Driven Development (SDD) workflow within Gemini CLI. This process prioritizes clear specifications and rigorous validation to ensure that all changes align with user requirements.

## Core Mandates

### 1. Specification First
- **Structure & Location:** Every project MUST maintain its specification in the `./docs/specification` folder. 
- **Persistent Specification:** `requirements.md`, `design.md`, and `test-strategy.md` are the source of truth and must be updated with every change.
- **Transactional Tasks:** Every story/epic must have a `tasks.md` in a `[seq]-[slug]` folder.
- **Validation:** Always verify requirements, design, and test strategy before starting implementation.

### 2. SDD Lifecycle
Follow this iterative cycle for every feature or bug fix:
1. **Research:** Understand the codebase and the persistent specification (`requirements.md`, `design.md`, `test-strategy.md`).
2. **Strategy:** Formulate a high-level strategy and update `design.md` and `test-strategy.md` if needed.
3. **Execution:** For each component defined in the transactional `tasks.md`:
   - **Plan:** Define implementation details and a testing strategy.
   - **Act:** Apply surgical, idiomatic code changes.
   - **Validate:** Run tests and linters to confirm the change matches the spec.

### 3. Verification & Validation
- **Unit Testing:** Add or update tests for every logic change.
- **Spec Compliance:** Perform a final review against the specification (requirements, design, and tasks) before concluding.

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
- `/sdd:init`: Initialize the project specification structure.
- `/sdd:requirements`: Define or update functional/non-functional requirements.
- `/sdd:design`: Define or update the implementation strategy.
- `/sdd:tasks`: Create an execution plan for a specific story or epic.
- `/sdd:check`: Analyze compliance with SDD mandates.

Refer to the **SDD Skill** (`skills/sdd/SKILL.md`) for complete workflow diagrams and implementation guidelines.
