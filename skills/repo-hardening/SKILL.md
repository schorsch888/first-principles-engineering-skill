---
name: repo-hardening
description: Review and harden repositories by running real build and test gates early, auditing contracts across component boundaries, turning validated findings into scoped fixes, and leaving repeatable validation evidence. Use when the user asks to review a repo or project, review这个项目, harden it to a stronger engineering standard, apply a FAANG standard or FAANG 标准, diagnose integration, runtime, or schema drift, or continue a review into implementation.
---

# Repository Hardening

## Core Rule

Ground conclusions in executable evidence. Run the smallest high-signal validation early, then let failures and system boundaries guide code inspection.

## FAANG-Grade Repository Bar

Interpret “FAANG standard” as evidence-backed production readiness, not checklist theater. Evaluate each applicable dimension and mark non-applicable ones with a reason:

- **Correctness and contracts:** reproducible build, lint, type, test, schema, migration, and integration evidence appropriate to the change.
- **Change safety:** bounded scope and explicit compatibility, dependency, data-migration, rollout, rollback, and blast-radius handling.
- **Security and privacy:** trust boundaries, authentication, authorization, secrets, dependency risk, input handling, and sensitive-data lifecycle.
- **Reliability and operability:** evidenced failure modes, resource bounds, concurrency behavior, health signals, logs, metrics, alerts, and recovery paths where relevant.
- **Maintainability and ownership:** clear owners, minimal accidental complexity, current contracts and runbooks, and focused checks at the defect boundary.
- **Delivery evidence:** exact commands and results, enforced CI/review gates, and explicit residual risks. Treat blocked or unrun checks as unknown.

Do not claim the repository clears this bar while an applicable critical or high-risk dimension lacks evidence.

## Workflow

1. Establish authority and scope.
   - Read repository instructions, contribution guidance, build manifests, CI configuration, and architecture records that govern the affected area.
   - Inspect `git status --short --branch`, relevant remotes, top-level structure, and component ownership.
   - Determine whether the user requested a read-only review or authorized remediation. Do not edit for a review-only request.

2. Build the validation map.
   - Identify existing build, lint, type, test, migration, container, and packaging gates before inventing new commands.
   - Check required tools and runtimes before costly investigation. Do not install dependencies or mutate the environment without task-appropriate authorization.
   - Run the fastest high-signal gates first. Record exact commands, results, and environmental blockers.

3. Audit contracts across boundaries.
   - Compare consumers with providers: routes and base URLs, schemas and migrations, types and nullability, configuration and environment variables, runtime versions, test discovery, and deployment artifacts.
   - Prefer current executable contracts and authoritative runtime sources over stale prose.
   - Classify material claims as observed fact, hard constraint, assumption, or unresolved evidence.

4. Fix the root boundary when authorized.
   - Trace affected callers and owners before editing; solve the defect once at the narrowest shared boundary.
   - Preserve data integrity, security, compatibility, and rollback constraints. Use explicit errors, transactional changes, migrations, or stable selectors only when the evidence requires them.
   - Add or update the smallest check that would have caught the defect. Preserve unrelated user changes.

5. Revalidate the result.
   - Rerun the failing or focused check, then the relevant broader gates.
   - Never report an unrun or blocked check as passed.
   - Add or repair scripts, CI gates, or active documentation only when needed to make required validation repeatable.

6. Hand off cleanly.
   - Report changed files, exact validation commands, results, and remaining blockers.
   - Use the repository's existing delivery workflow when publication is requested. Delegate to `propose-change` when it is available; keep forge-specific delivery policy out of this skill.

## Review Output

Lead with findings ordered by severity. Tie each finding to file and line evidence, explain impact, and identify the missing or failing check. If no findings are validated, state that directly and list residual risks or blocked validation.

For remediation, lead with the outcome and finish with changed files, validation evidence, and anything not verified.

## Guardrails

- Do not infer production readiness from static reading alone.
- Do not translate “stronger” or “FAANG standard” into speculative tooling, broad refactors, or checklist theater.
- Do not change code until the root cause and affected boundary are evidenced.
- Treat unavailable tools and services as unknown validation state, not success.
