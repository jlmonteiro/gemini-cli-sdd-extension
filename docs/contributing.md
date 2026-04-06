# Contributing Guide

This guide describes how to set up your local development environment and the standards to follow when contributing to the `sdd-extension`.

---

## 🛠 Local Environment Setup

To ensure all quality and validation tools (like Husky and `commitlint`) are correctly configured, follow these steps:

### 1. Clone the Repository
```bash
git clone https://github.com/jlmonteiro/gemini-cli-sdd-extension.git
cd gemini-cli-sdd-extension
```

### 2. Install Dependencies
Run the following command to install the development dependencies and **automatically initialize the Husky Git hooks**:

```bash
npm install
```

> **Important:** If you skip `npm install`, the commit validation hooks will not be active, which might lead to your pull requests being rejected by the automated release pipeline.

---

## 📜 Commit Standards

We use **Conventional Commits** to automate our versioning and release process. This is enforced locally via `commitlint` and Husky.

### Commit Format
```text
<type>(<scope>): <subject>

[optional body]

[optional footer(s)]
```

### Common Types
*   **feat:** A new feature (corresponds to a **Minor** version bump).
*   **fix:** A bug fix (corresponds to a **Patch** version bump).
*   **chore:** Maintenance tasks (e.g., updating dependencies).
*   **docs:** Documentation changes only.
*   **refactor:** A code change that neither fixes a bug nor adds a feature.
*   **test:** Adding missing tests or correcting existing tests.

### Breaking Changes
To indicate a **Major** version bump, add a `!` after the type/scope or include `BREAKING CHANGE:` in the footer.
Example: `feat!: change the command prefix to /spec`

---

## 🚀 Pull Request Guidelines

To ensure a smooth review process and maintain high project quality, please follow these guidelines for your Pull Requests (PRs):

### 1. Branch Naming
Create a new branch for every feature or fix. Use descriptive names with the following prefixes:
*   `feat/` for new features (e.g., `feat/add-new-persona`)
*   `fix/` for bug fixes (e.g., `fix/template-rendering`)
*   `docs/` for documentation updates
*   `chore/` for maintenance tasks

### 2. PR Title & Description
*   **PR Title:** Use the Conventional Commit format for your PR title (e.g., `feat(ui): add progress bars`).
*   **PR Description:** Clearly explain **what** was changed and **why**. If the change is complex, provide instructions on how to verify it.

### 3. Keep it Atomic
*   Aim for small, focused PRs that address a single concern.
*   Avoid mixing multiple features or unrelated bug fixes in a single PR. This makes reviews faster and safer.

### 4. Verify Locally
*   Before submitting your PR, ensure your local environment is clean and that you've run any relevant tests or validation tools.
*   Check that your commit messages follow the [Commit Standards](#-commit-standards) defined above.
*   **Automated Verification:** Every PR will trigger an automated GitHub Action that runs `gemini extensions validate .` to ensure the extension structure and manifest are correct.

---

## 🔄 Automated Release Process

When a commit is pushed to the `main` branch, our GitHub Action (`release.yml`) performs the following:
1.  **Analyzes Commits:** Uses `semantic-release` to calculate the next version based on the commit types.
2.  **Updates Metadata:** Synchronizes the `version` field in both `package.json` and `gemini-extension.json`.
3.  **Generates Changelog:** Updates `CHANGELOG.md` with the new version's notes.
4.  **Publishes Release:** Creates a new Git tag and a GitHub Release.
