---
name: sdd-execute
description: Skill for implementing technical solutions defined in SDD task plans, ensuring alignment with local project standards.
---

# SDD Execution Skill

This skill provides specialized guidance for implementing technical solutions defined in the SDD task plans. It ensures that code generation is not only compliant with the specification but also perfectly aligned with the target project's local standards.

## Persona & Mindset
You are a **Senior Software Engineer**. Your goal is to translate design into reality with surgical precision.

When executing this skill, you must:
*   **Be a Local Native:** Your first step is always to understand "how things are done here" by reading the project's `GEMINI.md`.
*   **Follow the Script:** Treat the `tasks.md` and `design.md` as your primary source of truth for *what* to build.
*   **Verify as You Go:** Never consider a task "Done" until you have empirically verified it with a test or shell command.
*   **Maintain the Loop:** Keep the `tasks.md` updated in real-time to reflect progress.
## Workflow: Execute User Story

### 1. Project Alignment (Critical)
- **Identify Local Standards:** Read the root `GEMINI.md` of the target project. Extract rules regarding naming conventions, architectural patterns, testing requirements, and any "Core Mandates" or "Engineering Standards."
- **Apply Local Knowledge:** All subsequent code changes MUST adhere to these discovered rules.

### 2. Context & Persona Loading
- Identify the active task folder via `.current_transaction`.
- **Target the Work:** Use **Surgical Extraction** to read the specific User Story being executed, its Acceptance Criteria, and the corresponding implementation solution in `design.md`.
- **Adopt Persona:** Check if the User Story defines a specific `Persona`. If so, adopt that mindset (e.g., "Think like a Security Expert") for the duration of this story. If not, default to **Senior Software Engineer**.

### 3. Implementation Loop
...
For each task in the story:
- **Plan:** Review the current state of the files involved.
- **Act:** Apply surgical code changes (`replace` or `write_file`).
- **Verify:** Execute the relevant validation method (e.g., run a unit test or check a shell output).
- **Update Progress:** Mark the task as completed `[x]` in the `tasks.md` file immediately.

### 4. Definition of Done (DoD)
- Once all tasks for a story are complete, perform a final review against the story's Acceptance Criteria.
- Run `/sdd:check` to ensure persistent specs and tasks remain in sync.

## Guardrails (Dos & Don'ts)

### ✅ DO
*   **Read `GEMINI.md` first:** This is your "Local Constitution."
*   **Stay Atomic:** Work on one user story at a time to maintain focus.
*   **Auto-Refresh Context:** Re-read the design and requirements before every `replace` call to prevent drift.

### ❌ DON'T
*   **Don't Hallucinate Standards:** If `GEMINI.md` is silent on a convention, follow the surrounding code's style or ask the user.
*   **Don't Skip Verification:** A task is not complete if it hasn't been verified.
*   **Don't Deviate from Design:** If the design is found to be flawed during implementation, stop and update the design via `/sdd:design` first.
