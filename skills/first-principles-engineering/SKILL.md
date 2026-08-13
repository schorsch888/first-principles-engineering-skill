---
name: first-principles-engineering
description: Reframe engineering requirements, issues, architecture decisions, bugs, and remediation plans from current evidence, desired outcomes, hard constraints, invariants, ownership, state transitions, and acceptance evidence. Use when the user asks for “第一性原理” or “first-principles” analysis, asks whether issues overlap or duplicate each other, wants to identify the root problem, challenge inherited scope or assumptions, rewrite an issue/spec around current truth, or derive the smallest defensible solution before implementation.
---

# First-Principles Engineering

## Core Rule

Derive the decision from observable current state and the intended outcome. Treat existing titles, issue structure, documentation, implementations, and historical plans as evidence—not axioms.

## Workflow

1. State the decision or question in one sentence.
   - Express the target as an observable outcome, not a preferred implementation.
   - Identify whose state, behavior, or responsibility must change.

2. Build the evidence model.
   - Inspect the current authoritative sources before concluding: code, runtime behavior, tests, issue state, contracts, ADRs, or external decisions as applicable.
   - Classify relevant claims as fact, hard constraint, assumption, or prior decision.
   - Verify mutable sources are current; do not promote historical truth into present truth.

3. Reconstruct only the fundamentals needed for the decision:
   - desired outcome;
   - current state;
   - hard constraints and invariants;
   - ownership and system boundary;
   - required state transition;
   - observable acceptance evidence.

4. Challenge inherited structure.
   - Separate requirements from implementations, dependencies from shared prerequisites, current truth from history, and safety constraints from conventions.
   - Ask what would still be required if the existing solution or issue hierarchy did not exist.
   - Remove stale, duplicate, and speculative scope while preserving unique evidence and non-negotiable constraints.

5. Select the smallest defensible change.
   - Solve the root problem at the narrowest shared boundary.
   - Reuse an existing mechanism when it satisfies the derived constraints.
   - State unresolved facts explicitly. If no change is required, say so.

6. Validate the derivation.
   - Tie each material conclusion to evidence.
   - Map each proposed change to an acceptance check.
   - Run relevant checks when implementation is requested. For repository-wide review or remediation, use `validation-first-repo-hardening` after framing the problem when that skill is available.

## Output

Lead with the conclusion. Show only the derivation needed to audit it: facts, constraints, rejected assumptions, resulting decision, and verification.

When rewriting an issue or specification, prefer this minimal structure:

- Current truth
- Outcome
- Scope and non-goals
- Invariants
- Acceptance evidence
- Dependencies or blocked decisions

Preserve comments or history that carry unique audit or acceptance evidence. Delete them only when their evidence is retained elsewhere and they are genuinely obsolete.

## Guardrails

- Do not use “first principles” as permission to ignore prior art or rewrite working systems.
- Do not invent facts, treat missing evidence as proof, or discard explicit safety, security, accessibility, validation, or data-integrity constraints.
- Do not turn the response into a philosophical essay; derive only what changes the decision.
- Skip the full framework for routine, already well-specified work.
