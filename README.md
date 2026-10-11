# AI Developing Conduction

A reusable GitHub template for **human-directed, AI-executed Java/Maven development**.

## How it works

**Human feature idea → AI Product Manager (User Story) → AI Developers (Tasks + task branches) → AI Integration (story branch) → AI QA → AI Pull Request → Human review/merge/release.**

The AI must use the supplied GitHub templates and project coding standards. The AI **never** merges to `main` or publishes a release.

## Getting started

1. Mark this repository as a **Template repository** in GitHub, then create a new repository from it.
2. Adjust `pom.xml` group/artifact IDs and Java version for the new project.
3. Create the GitHub labels: `user-story`, `task`, `bug`, `spike`, `qa-failed`, `qa-passed` (see `.github/labels.md`).
4. Enable branch protection / repository rulesets for `main`: require PR, human approval and passing CI.
5. Give the agent permission to create issues, branches and PRs **only** in this repository; do not grant merge, tag or release permissions if avoidable.
6. Configure a real workspace sandbox with appropriate access for Maven/JDK/Git and controlled GitHub networking. `AGENTS.md` alone is not a security boundary.
7. Start a chat with a feature idea and ask the agent to follow `AGENTS.md`.

## Repository contents

- `AGENTS.md` — binding agent instructions and boundaries
- `.ai/roles/` — Product Manager, Developer, QA, human Release Manager
- `.ai/workflows/` — feature and defect workflows
- `.ai/standards/` — Java, Clean Code, testing, formatting, Git conventions
- `.github/ISSUE_TEMPLATE/` — User Story, Task, Bug Report, Spike
- `.github/PULL_REQUEST_TEMPLATE.md` — one PR per User Story
- `.github/workflows/ci.yml` — Maven CI verification
- `pom.xml` — minimal Java 21 / JUnit 5 starter (customize as needed)

## Branch example

`main` (protected) → `story/42-user-export` → `task/43-api` and `task/44-pagination` → integrate into `story/42-user-export` → QA → PR into `main` → **human merge**.

Task branches are based on the story branch and merged back into it only after passing their own tests. Do not open multiple PRs for the same story. Do not merge task branches into `main`.

## Local verification

```bash
mvn verify
```

The included Maven starter provides JUnit 5 and Surefire. Replace the example package identifiers before using it for production code.

## Operational notes

- Issue templates use GitHub's YAML frontmatter; agents should remove frontmatter when posting issue bodies via API/CLI.
- `gh issue create` / `gh pr create` require a pre-authorized GitHub CLI or equivalent connector. Never inspect credential files.
- Maven typically reads a JDK installation and dependency cache outside the repo; a strict sandbox must explicitly provide those resources or project-local equivalents. This policy does not imply that Maven can run in a totally isolated filesystem without preparation.
- CI runs on GitHub-hosted runners and has its own workspace; it is not subject to a local agent sandbox.
- A task requiring an out-of-scope operation is **BLOCKED**, not permission to work around the restriction.
