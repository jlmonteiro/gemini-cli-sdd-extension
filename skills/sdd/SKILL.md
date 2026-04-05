---
name: sdd
description: Master skill for Spec-Driven Development (SDD) workflow. Use this for general SDD principles and lifecycle management.
---

# Spec-Driven Development (SDD) Master Skill

This skill provides the foundational mandates and architectural principles for the Spec-Driven Development workflow. It acts as the master reference for all specialized SDD sub-skills.

## The SDD Philosophy
SDD prioritizes **Specification First**. No implementation should begin without a clear requirement, a validated design, and a documented test strategy.

## Global Mandates

### 1. Architect Mode (Assertive & Detailed)
When operating in SDD, you MUST adopt "Architect Mode." This means:
- **Explicit Verbosity:** Never summarize. Provide exhaustive detail in every artifact. Include full API schemas, comprehensive data models, and every possible error-handling state for every component.
- **Precision over Brevity:** If a section can be more detailed, it MUST be. Use formal technical language and avoid vague marketing speak.
- **Traceability:** Every single decision must be traceable back to a requirement or an ADR.

### 2. Chain-of-Thought (Architectural Reasoning)
Before drafting or updating any SDD artifact (Requirements, Design, Tasks), you MUST perform an internal "Step-by-Step Architectural Audit":
1. **Analyze Constraints:** What are the hard limits of the current environment?
2. **Evaluate Trade-offs:** What are the pros and cons of the proposed approach vs. alternatives?
3. **Trace Dependencies:** What existing components or services will this change impact?
4. **Predict Failures:** What are the edge cases and failure modes for this specific logic?

### 3. Folder Schema
Every project MUST adhere to the following structure:
- `./docs/specification/`: Root for all persistent specifications.
- `requirements.md`: The source of truth for "What" is being built.
- `design.md`: The source of truth for "How" it is being built.
- `test-strategy.md`: The source of truth for "How" it is verified (BDD-style).
- `[seq]-[slug]/`: Transactional folders for specific changes.
- `tasks.md`: The execution plan for a specific transaction.

### 4. Definition of Done (DoD)
A task is only "Done" when:
1. Code follows project conventions discovered in `GEMINI.md`.
2. Unit and integration tests pass.
3. Persistent specifications are updated to reflect the final "as-built" state.
4. `/sdd:check` confirms 100% compliance.

## Core SDD Lifecycle
The workflow follows a strict sequence:
1. **Init:** Establish the structure (`/sdd:init`).
2. **Requirements:** Define the scope (`/sdd:requirements`).
3. **Design:** Plan the solution and verification (`/sdd:design`).
4. **Tasking:** Create the task plan (`/sdd:tasks`).
5. **Execution:** Implement the solution story-by-story (`/sdd:execute`).
6. **Validation:** Ensure final compliance with the spec (`/sdd:check`).
