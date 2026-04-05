# Spec-Driven Development (SDD) Extension Documentation

## 🏗 Architecture

The `sdd-extension` is built using a **Thin Command / Fat Skill** architecture. This ensures that the agent's instructions are modular, lazy-loaded, and highly specialized for the task at hand.

### Personas & Mindsets
Every phase of the SDD lifecycle is guided by a specific professional persona:
- **Requirements:** Senior Product Owner & Analyst.
- **Design:** Senior Systems Architect.
- **Tasking:** Senior Project Manager & Scrum Master.
- **Execution:** Senior Software Engineer (Local Native).
- **Validation:** Senior QA Engineer & Compliance Auditor.

---

## 🔄 Core Workflow

### 1. Project Initialization (`/sdd:init`)
The `sdd-init` skill acts as an orchestrator. It performs an environmental analysis and delegates document creation to 
the `sdd-requirements` and `sdd-design` skills. It supports **Retroactive Inspection** for existing codebases.

### 2. Requirements Discovery (`/sdd:requirements`)
Guided by the Product Owner persona, this phase captures:
- **Business Context & Stakeholders:** The "Why" and "Who."
- **Out of Scope:** Explicit boundaries to prevent creep.
- **User Journeys:** Behavioral flows through the feature.

### 3. Solution Design (`/sdd:design`)
The Architect persona synthesizes a solution including:
- **Architecture Visuals:** Mermaid diagrams for components and data flow.
- **Cross-Cutting Concerns:** Error handling, security, and observability.
- **BDD Scenarios:** Given/When/Then scenarios for verification.

### 4. Transactional Planning (`/sdd:tasks`)
Work is broken down into a `[seq]-[slug]/tasks.md` plan:
- **Definition of Ready (DoR):** Verifies the design is mature before starting.
- **Critical Path:** Identifies sequencing and parallelism.
- **Technical Risks:** Proactive mitigation strategies.

### 5. High-Rigor Execution (`/sdd:execute`)
The Engineer implements the plan by:
- **Local Alignment:** Reading the target project's `GEMINI.md`.
- **Incremental Refresh:** Re-reading specs before every surgical edit.
- **Automated Update:** Marking tasks as `[x]` in real-time.

### 6. Compliance Audit (`/sdd:check`)
The Auditor ensures the "Golden Thread" of traceability remains unbroken:
- **Content Integrity:** Removing template residue.
- **Bi-Directional Traceability:** Requirements -> Design -> Tests -> Tasks.

---

## 🛡 Optimization Guardrails

- **Sub-Agent Delegation:** Uses `codebase_investigator` for complex architectural mapping.
- **Tool Hierarchy:** Prioritizes `glob` and `grep_search` over expensive directory listings.
- **Surgical Extraction:** Uses `start_line` and `end_line` to keep context windows lean.
- **Transaction Identity:** Maintains state across sessions via `.current_transaction`.

---

## 📖 Templates
All generated documents are based on standardized structures found in the `templates/sdd/` directory.
