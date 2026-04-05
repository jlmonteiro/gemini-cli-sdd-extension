---
name: sdd-init
description: Skill for initializing an SDD workspace, including retroactive codebase inspection and specification generation.
---

# SDD Initialization Skill

This skill provides specialized guidance for initializing a Spec-Driven Development (SDD) workspace. It acts as an orchestrator, delegating specific document creation to its respective specialized skills.

## Workflow: Retroactive Initialization

When initializing a project with an existing codebase, follow these steps to ensure a high-quality specification is generated:

### 1. Environmental Analysis (Assertive Discovery)
- **Multi-Module Detection:** Immediately identify if the project is a monorepo or has multiple distinct modules (e.g., `/frontend`, `/backend`, `/core`).
- **Framework & Tech Stack Identification:** For each identified module, inspect package managers and build files (e.g., `package.json`, `go.mod`, `pom.xml`, `requirements.txt`, `Cargo.toml`). You MUST extract the specific frameworks and core libraries being used (e.g., React, Mantine, TanStack Query, Express, Spring Boot).
- **Sub-Agent Delegation:** For large or complex codebases, **delegate discovery to the `codebase_investigator` sub-agent**. Provide it with a detailed objective: "Map the project structure, identify ALL distinct modules, extract the technical stack (frameworks, libraries, build tools) for each module, and summarize core components for SDD specification generation."
- For small, simple projects, use `list_directory` and `read_file` directly.
- Identify the project name and primary programming languages.
- Map the high-level folder structure.

### 2. Requirements Extraction (Delegate)
- **Activate the `sdd-requirements` skill.**
- Instruct the agent to perform a retroactive analysis of the codebase to extract Functional Requirements (FRs), Non-Functional Requirements (NFRs), and ADRs based on the tech stack and modules discovered in step 1.
- Create the initial `requirements.md` based on this analysis.

### 3. Design Reconstruction (Delegate)
- **Activate the `sdd-design` skill.**
- Instruct the agent to analyze the implementation to document the strategy, components, and data model. The design MUST explicitly reflect the multi-module nature and the specific frameworks (e.g., "Frontend uses Mantine for UI and TanStack for data fetching") discovered in step 1.
- Create the initial `design.md` that reflects the "as-built" architecture.

### 4. Test Strategy Mapping (Delegate)
- **Activate the `sdd-design` skill** (which also handles test strategy).
- Instruct the agent to identify existing tests and map them to the extracted requirements.
- Create the initial `test-strategy.md` with BDD-style scenarios for existing features.

### 5. Finalization
- Inform the user that the specification has been retroactively generated through the specialized skills.
- Suggest using `/sdd:check` to verify the new structure.

## Workflow: Empty Project Initialization
- Create the `./docs/specification/` folder.
- **Activate the `sdd-requirements` skill** to start the fresh requirements gathering process.

## Resources
- This skill MUST NOT create `requirements.md`, `design.md`, or `test-strategy.md` directly. It MUST always delegate to the specialized skill for that file type.
