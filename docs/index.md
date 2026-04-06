# Spec-Driven Development (SDD) Extension Documentation

The `sdd-extension` transforms Gemini CLI into a high-rigor, professional engineering partner. It enforces a strict "Specification-First" workflow, ensuring that every code change is grounded in requirements, architecture, and a verified test strategy.

---

## 🚀 Installation & Setup

### 1. Install from GitHub
Install the extension directly into your Gemini CLI environment:

```bash
# In your terminal
gemini extension install https://github.com/jlmonteiro/gemini-cli-sdd-extension
```

### 2. Verify Installation
Once installed, verify that the extension and its commands are correctly registered:

```bash
# List all active extensions
gemini extension list

# Verify the available /sdd commands
gemini help sdd
```

**Expected Verification Output:**
- `sdd-extension` should appear in the extension list.
- `help sdd` should list: `/sdd:init`, `/sdd:requirements`, `/sdd:design`, `/sdd:tasks`, `/sdd:execute`, and `/sdd:check`.

---

## 🔄 Command Guide & Examples

### 1. Initialize Project (`/sdd:init`)
Establishes the SDD folder structure. If the project already has code, the **Architect** persona will retroactively inspect it to generate an "as-built" specification.

*   **Usage:** `/sdd:init`
*   **Expected Output:**
    - Creates `./docs/specification/` directory.
    - Generates initial `requirements.md`, `design.md`, and `test-strategy.md`.
    - **Architect's Summary:** "I have mapped your multi-module Java/React project. I identified Spring Boot 3.x and Mantine UI as core frameworks. Specification documents have been retroactively generated."

### 2. Define Requirements (`/sdd:requirements`)
The **Senior Product Owner** persona initiates a proactive, structured dialogue to capture and **refine** the "What" and "Why."

*   **Usage:** `/sdd:requirements "Add JWT authentication to the API"`
*   **Interactive Workflow:**
    - **Context & Gap Analysis:** Gemini asks for the high-level context and **proactively suggests** improvements or identifies missing requirements based on best practices.
    - **Actor Discovery:** "Who are the primary actors? (e.g., Admin, Registered User)."
    - **NFR Suggestions:** Explicitly prompts for **Observability**, **Reliability**, **Performance**, and **Security** needs.
*   **Expected Output:**
    - Updates `./docs/specification/requirements.md` with refined FRs, NFRs, and mapped Actors.
    - **PO's Summary:** "I've refined your request by adding FR-5 (JWT Authentication) and suggested two additional NFRs for token rotation and audit logging which we've now included."

### 3. Solution Design (`/sdd:design`)
Synthesizes the technical "How" based on requirements.

*   **Usage:** `/sdd:design`
*   **Architect Mode:** Gemini will "Think step-by-step" to rationalize framework choices and data flow.
*   **Expected Output:**
    - Updates `design.md` with component layers, API schemas, and Mermaid diagrams.
    - Updates `test-strategy.md` with BDD scenarios (Given/When/Then).
    - **Architect's Summary:** "I've designed the JWT layer. It uses a custom `AuthFilter` in the Backend and `TanStack Query` for token state in the Frontend. I've also added 3 BDD scenarios to verify the login flow."

### 4. Transactional Tasking (`/sdd:tasks`)
Decomposes the design into an actionable, transactional execution plan.

*   **Usage:** `/sdd:tasks "US-10: JWT Implementation"`
*   **Expected Output:**
    - Creates `./docs/specification/01-jwt-implementation/tasks.md`.
    - Creates a `.current_transaction` file pointing to this folder.
    - **Scrum Master's Summary:** "Plan created with 5 implementation tasks. I've identified a risk regarding CORS configuration with JWT, which we'll mitigate in task 3."

### 5. High-Rigor Execution (`/sdd:execute`)
Atomically implements the tasks in the active plan.

*   **Usage:** `/sdd:execute` or `/sdd:execute US-1`
*   **Execution Logic:** Gemini adopts the **Senior Engineer** persona, reads the local `GEMINI.md` for standards, and implements one task at a time.
*   **Expected Output:**
    - Surgical code changes applied to files.
    - Tests executed to verify each change.
    - `tasks.md` updated with `[x]` for completed items.

### 6. Compliance Check (`/sdd:check`)
The **Auditor** persona verifies the integrity and traceability of the entire specification.

*   **Usage:** `/sdd:check`
*   **Expected Output:**
    - **Compliance Report:**
        - ✅ Structural Integrity (All files present).
        - ❌ Traceability Gap: Requirement FR-5 has no corresponding BDD scenario in `test-strategy.md`.
        - ✅ Template Residue (No placeholders found).
    - **Auditor's Advice:** "Please run `/sdd:design` to generate the missing BDD scenario for FR-5."

---

## 🏗 Architecture & Personas

The extension uses a **Thin Command / Fat Skill** architecture. Commands are simple entry points, while the intelligence resides in specialized **Agent Skills**:

| Persona | Skill | Mindset |
| :--- | :--- | :--- |
| **Product Owner** | `sdd-requirements` | Value-driven, protective of scope, interactive. |
| **Architect** | `sdd-design` | Detail-oriented, rationalizes trade-offs, visual. |
| **Scrum Master** | `sdd-tasks` | Predictable, risk-aware, focuses on "Done." |
| **Engineer** | `sdd-execute` | Local native, surgical, verification-first. |
| **Auditor** | `sdd-check` | Skeptical, demands traceability, binary quality. |

---

## 🛡 Optimization Guardrails

- **Context Efficiency:** Uses `codebase_investigator` for broad analysis but switches to `grep_search` and `read_file` (with line ranges) for surgical implementation.
- **Transaction Safety:** Uses `.current_transaction` to ensure multiple sessions or agents stay aligned on the same unit of work.
- **Local Alignment:** Always prioritizes instructions found in the root `GEMINI.md` of the target project to ensure generated code matches existing conventions.
