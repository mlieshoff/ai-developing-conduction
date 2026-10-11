# AI Developing Conduction — Agent Contract

This file is the mandatory entry point for AI-assisted development in this repository.
The current repository root (`git rev-parse --show-toplevel`) is the workspace boundary.
Follow these instructions and read the linked role, workflow and standards files before acting.

## Non-negotiable rules

1. **Workspace boundary:** Never intentionally read, list, search, create, modify or delete files outside the repository root, including parent/sibling directories, home files, and symlinks resolving outside the root. Do not run unreviewed scripts that violate this rule. If a tool requires external filesystem access, stop and request a specifically scoped exception. This file is policy, **not** an OS sandbox; configure actual sandbox enforcement separately.
2. **Git safety:** Never commit or push to `main`, force-push, rewrite history, discard user changes, or bypass protection rules. If working tree is dirty, ask before switching branches or modifying existing changes.
3. **Human authority:** AI may create GitHub issues, task branches, commits, pushes and **one pull request per story**. Only a human may approve/merge PRs, tag, release or deploy.
4. **Scope:** Do not modify unrelated files, upgrade dependencies, alter CI/infrastructure or database schemas without explicit approval. Do not introduce new dependencies without approval.
5. **Verification:** Add meaningful unit/regression tests, run Maven verification and report exact results. Never suppress failures or claim success without evidence.
6. **Templates:** Use repository templates in `.github/ISSUE_TEMPLATE/` and `.github/PULL_REQUEST_TEMPLATE.md`. Preserve their sections when composing GitHub issue/PR bodies.
7. **Secrets:** Never print, store or commit credentials, tokens, personal data or secrets. Never access global Git/SSH settings or credentials directly. Use only preconfigured, authorized GitHub tooling.
8. **Ambiguity:** Ask the user before making material product, security, architecture or destructive decisions. Otherwise proceed autonomously within scope.

## Mandatory lifecycle

Follow `.ai/workflows/feature-development.md`:

1. **Product Manager:** Read `.ai/roles/product-manager.md`. Transform feature prompt into a User Story GitHub issue using `user-story.md`; define testable acceptance criteria.
2. **Development:** Read `.ai/roles/developer.md`. Create Task issues using `task.md`. Develop each task on its own branch, starting from the story integration branch (or an agreed base); implement Java and JUnit tests; commit and push.
3. **Integration:** Integrate task branches into one `story/<issue-number>-<slug>` branch, **never main**. Resolve conflicts without losing changes; run verification.
4. **QA:** Read `.ai/roles/qa.md`. Independently validate story acceptance criteria and run tests; record PASSED / FAILED / BLOCKED. On failure return to development; do not create a ready-for-review PR until QA passes.
5. **PR & handover:** Create exactly one PR per story from story branch into `main` using the PR template. Link the story and tasks; include verification evidence and risks. Human reviews and merges. **Stop.**
6. **Release:** Human-only; `.ai/roles/release-manager.md` is guidance for the human, not an AI execution role.

## Coding standards

Read and apply `.ai/standards/java.md`, `.ai/standards/testing.md`, `.ai/standards/formatting.md`, `.ai/standards/clean-code.md`, `.ai/standards/git.md`.
Use Java and Maven. Prefer `./mvnw` when present, otherwise `mvn`. Execute `verify` without skipping tests.

## Execution and reporting

Before work: state planned issue/branch structure and any blocking questions.
At handover: provide story issue, task issues, branch, commit IDs, PR URL, test commands/results, QA status and residual risks.
Do not automatically close issues or mark a release complete. GitHub API/network access requires separately granted credentials and permissions.

## Architecture Standards

All AI roles MUST follow the architectural rules defined in:

`.ai/standards/architecture.md`

The Development Team MUST preserve the existing architecture.

The QA agent MUST verify architectural compliance before
the Pull Request is marked ready for human review.

Significant architectural changes require explicit human approval.