---
name: propose-change
description: Prepare and publish consistent GitLab merge requests and GitHub pull requests as auditable change proposals with reusable descriptions, risk and review-effort labels, evidence-based target selection, focused validation, and safe post-merge branch/worktree cleanup. Use when creating or standardizing an MR/PR, configuring shared review templates or labels, choosing a target branch, promoting an integration branch to a stable branch, or cleaning up after merge. Leave CI/check monitoring, review decisions, and merge execution to the repository's established workflow or a compatible status skill.
---

# Propose Change

Create one auditable, self-contained proposal for review on either forge. Reuse repository policy and native forge features before adding configuration.

## Boundaries

- Own preflight, target selection, title/body, labels, publishing, and post-merge cleanup.
- Hand CI/check status, review state, failure triage, auto-merge, and merge execution to the repository's workflow or a compatible status skill such as `ci-status-snapshot` when available.
- Do not stage unrelated changes, expose secrets, overwrite stronger repository policy, or mutate repository labels during routine submission.

## 1. Inspect Before Writing

1. Read repository instructions, contribution guidance, CODEOWNERS, existing templates, and protected-branch conventions.
2. Detect GitLab or GitHub from the push remote. Verify the matching `glab` or `gh` authentication before publishing.
3. Inspect the current branch, upstream, `git status --short --branch`, worktree ownership, and the complete diff against the candidate target.
4. Stop if the source equals the target, the target does not exist, or the diff is empty.
5. Separate unrelated concerns. Treat review-effort 5 as a split signal unless the change is intrinsically atomic.
6. Run the smallest repository-required validation that proves the changed behavior. Record exact commands and outcomes; never imply an unrun check passed.

## 2. Select the Target Explicitly

Apply this precedence:

1. Use an explicit user target when valid.
2. Otherwise follow written repository policy.
3. Otherwise infer an established integration-to-stable flow from recent merged requests and branch protections: normal work targets the integration branch; only release/promotion requests target the stable branch.
4. Otherwise target the remote default branch.

Never infer from the local branch name alone. A hotfix directly to a stable branch requires explicit authorization plus a reconciliation plan for the integration branch. If evidence conflicts, stop before publishing and ask for the target.

## 3. Build the Review Packet

- Use `assets/change-request.md` for normal changes and `assets/release-request.md` for integration-to-stable promotions.
- Write an imperative, Conventional Commit-style title that describes the actual change.
- Explain why the change exists, what changed, and what is intentionally out of scope.
- Include compatibility and risk, actual validation evidence, rollout, observability, and rollback.
- Use closing keywords only when the request completes the linked work item's acceptance criteria.
- Choose exactly one review-effort label and one risk label from `references/labels.md`. Add existing project-specific area labels only when useful.
- Prefer draft status for incomplete validation, requested early review, or high/critical risk. Otherwise publish ready for review when the user requested submission.

## 4. Publish With Explicit Inputs

1. Confirm the exact staged paths and resulting commit before pushing. Preserve unrelated dirty files.
2. Push the source branch with upstream tracking.
3. Create the request with explicit source, target, title, template/body, labels, and draft state:
   - GitHub: use `gh pr create --base ... --head ... --title ... --body-file ...` and label flags, or reuse `github:yeet` for the mechanical commit/push/create steps if available.
   - GitLab: use `glab mr create --source-branch ... --target-branch ... --title ... --template ... --label ... --remove-source-branch` or an equivalent structured API payload.
4. Pass body text as a file, native template, or structured argument. Never interpolate untrusted body text into a shell command.
5. Report the URL, source and target, head SHA, selected labels, validation evidence, and any missing repository configuration.
6. If the user asks to wait, merge, or diagnose CI, hand the created request to the repository's workflow or a compatible status skill; do not implement a second polling or merge workflow here.

## 5. Configure a Repository Only When Asked

Preserve stronger existing checks and show the diff before replacing any template.

- GitLab: install the normal and release assets as `.gitlab/merge_request_templates/Default.md` and `.gitlab/merge_request_templates/Release.md`.
- GitHub: install the normal asset as `.github/PULL_REQUEST_TEMPLATE.md` and the release asset as `.github/PULL_REQUEST_TEMPLATE/release.md`.
- Prefer an organization/group-level template or label definition when the forge and plan support it; otherwise configure each repository.
- Create the canonical labels in `references/labels.md` only with explicit repository-configuration authorization. During routine submission, reuse an accepted alias; if neither exists, state the missing label instead of silently changing repository settings.

## 6. Clean Up Only After Authoritative Merge Evidence

1. Keep the branch and worktree while the request is open or under review. Prefer provider-side source-branch deletion after merge.
2. Read fresh authoritative request state once and verify `merged`, the exact source branch, and the merged head SHA.
3. Require a completely clean local worktree, including untracked files. Remove only a worktree created or explicitly owned by this task, and run removal from outside it.
4. Delete the local branch with `git branch -d` first. Force deletion only when exact-head merge evidence exists and cleanup was explicitly requested.
5. Preserve closed/unmerged branches and worktrees unless the user explicitly confirms discarding the identified commits.
6. Never clean sibling branches, host-managed worktrees, or unrelated repositories.
