## Behavioral Guidelines

### Think & Plan
- State assumptions, list interpretations, default to simplicity.
- Fix FIRST; ask before proposing broader refactors or enhancements.

### Implementation Discipline
- NEVER implement unrequested features; limit changes to the active prompt.
- Use direct code (refactor on duplication); touch only logical path files.
- Match project style by inspecting adjacent files; remove unused variables/imports.
- Default environments/toggles to PROD when variables are missing.
- DIFF-AS-RECEIPT: Every edit turn MUST include a git diff in a collapsible `<details>` block.

### Verification
- Define success criteria and verify in terminal (`ls`, `git status`) before marking done.
- State a brief plan with verification checks for multi-step tasks.

### Dependencies & Solutions
- No dependencies for logic <20 lines. Libraries only for complex/high-risk tasks; verify they are lightweight and maintained.
- ZERO SPECULATION: Verify APIs via search/run command. No guessing, no abstract/clever solutions unless established.

### Fail Fast
- No silent fallbacks or rescue scripts. Hard stop (`return`/`throw`/`exit`) with a clear error on failed preconditions.

## Standards

### Hard Stops
- NEVER branch from a feature branch; always start from `origin/main`.
- NEVER push to main or merge PRs; leave merging to humans.
- NEVER rewrite history (`rebase -i`, `--squash`).
- NEVER use triple-backticks; wrap code/manifests in 4-backtick blocks.
- NEVER commit credentials, secrets, or PII.
- NEVER silence diagnostics (`eslint-disable`, `@ts-ignore`); fix the root cause.
- NEVER delete failing tests; fix the code.
- NEVER run `oc` commands. OpenShift access is restricted.
- NEVER impersonate human contributors or use credentials to post.
- NEVER use `--legacy-peer-deps`; resolve peer conflicts cleanly.
- NEVER execute vague or high-risk prompts without explicit user approval.

### Operational Guardrails
- Push and open PRs to feature branches without asking. Never mark work complete until verified, committed, pushed, and PR created.
- Stop on the first error; chain related commands with `&&`.
- Block SQL injection, XSS, and unsanitized inputs in code and docs.
- Temporary storage: `./.tmp/` if git-ignored, otherwise `/tmp`.

### Git Workflow
1. Branch: `git fetch origin && git checkout -b feat/name origin/main && git push -u origin HEAD`.
2. PR: `unset GITHUB_TOKEN && gh pr create --fill`.
3. Update: Always fetch and merge `origin/main` before new edits or pushing.
4. Close: Use `Closes #<num>` ONLY if an issue is explicitly provided. Never guess.

### Project Standards
- Conventional Commits. Latest stable packages; never downgrade or edit lock files silently.
- Minimum permissions (e.g., `permissions: {}` in GitHub Actions). No manual version tracking artifacts.

### Model Complexity

CRITICAL: Warn on tier mismatch at response start and end.

- **T1 (Trivial)**: Typos, formatting, basic scripts.
- **T2 (Standard)**: Features, refactors, tests.
- **T3 (Architecture)**: System design, multi-repo.
