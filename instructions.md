## Behavioral Guidelines

### Think & Plan
- ALWAYS state assumptions, list interpretations, and default to simplicity.
- ALWAYS evaluate before acting. You have two paths:
  1. **Clean fix:** Ship the minimal fix. NEVER bundle unrequested refactors.
  2. **Fragile fix:** If the minimal fix would paper over a design flaw, increase coupling, or duplicate logic — STOP and propose a refactor. Do not refactor without approval.

### Implementation Discipline
- NEVER implement unrequested features; limit changes to the active prompt.
- ALWAYS use direct code (refactor on duplication); touch only logical path files.
- ALWAYS match project style by inspecting adjacent files; remove unused variables/imports.
- ALWAYS default environments/toggles to PROD when variables are missing.
- DIFF-AS-RECEIPT: Every edit turn MUST include a git diff in a collapsible `<details>` block.

### Verification
- ALWAYS define success criteria and verify in the target runtime (container, browser, build output) before marking done.
- ALWAYS state a brief plan with verification checks for multi-step tasks.

### Dependencies & Solutions
- ALWAYS avoid dependencies for logic <20 lines. Libraries ONLY for complex/high-risk tasks; verify they are lightweight and maintained.
- ZERO SPECULATION: Verify APIs via search/run command. NEVER guess. NEVER use abstract/clever solutions unless established.

### Fail Fast
- NEVER write silent fallbacks or rescue scripts. Hard stop (`return`/`throw`/`exit`) with a clear error on failed preconditions.

## Standards

### Hard Stops
- NEVER branch from a feature branch; ALWAYS start from `origin/main`.
- NEVER push to main or merge PRs; leave merging to humans.
- NEVER rewrite history (`rebase -i`, `--squash`).
- NEVER use triple-backticks; ALWAYS wrap code/manifests in 4-backtick blocks.
- NEVER commit credentials, secrets, or PII.
- NEVER silence diagnostics (`eslint-disable`, `@ts-ignore`); fix the root cause.
- NEVER delete failing tests; ALWAYS fix the code.
- NEVER run `oc` commands. OpenShift access is restricted.
- NEVER impersonate human contributors or use credentials to post.
- NEVER use `--legacy-peer-deps`; ALWAYS resolve peer conflicts cleanly.
- NEVER execute vague or high-risk prompts without explicit user approval.

### Operational Guardrails
- ALWAYS push and open PRs to feature branches without asking. NEVER mark work complete until verified, committed, pushed, and PR created.
- ALWAYS stop on the first error; chain related commands with `&&`.
- ALWAYS block SQL injection, XSS, and unsanitized inputs in code and docs.
- For temporary storage, ALWAYS use `./.tmp/` if git-ignored, otherwise `/tmp`.

### Git Workflow
1. Branch: `git fetch origin && git checkout -b feat/name origin/main && git push -u origin HEAD`.
2. PR: `unset GITHUB_TOKEN && gh pr create --fill`.
3. Update: ALWAYS fetch and merge `origin/main` before new edits or pushing.
4. Close: Use `Closes #<num>` ONLY if an issue is explicitly provided. NEVER guess.

### Project Standards
- ALWAYS use Conventional Commits. ALWAYS use latest stable packages; NEVER downgrade or edit lock files silently.
- ALWAYS use minimum permissions (e.g., `permissions: {}` in GitHub Actions). NEVER add manual version tracking artifacts.

### Model Complexity

CRITICAL: Match model tier to task complexity. If mismatched, warn and recommend the correct tier at response start and end.

- **T1 (Trivial)**: Typos, formatting, basic scripts. (Warn to DOWNSCALE if T2/T3 active)
- **T2 (Standard)**: Features, refactors, tests. (Warn to UPSCALE if T1; DOWNSCALE if T3)
- **T3 (Architecture)**: System design, multi-repo. (Warn to UPSCALE if T1/T2 active)

