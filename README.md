# First-Principles Engineering

Evidence-led engineering skills for framing decisions and hardening repositories.

“FAANG-grade” means an auditable, production-grade quality bar across the dimensions that apply—not a universal company checklist or extra ceremony.

The repository contains two shared skills and native plugin metadata for both Claude Code and Codex:

- `engineering`: derive the smallest defensible decision and verify its production implications.
- `repo-hardening`: review and remediate repositories against evidence-backed readiness dimensions.

## Claude Code

```text
/plugin marketplace add schorsch888/first-principles-engineering-skill
/plugin install first-principles@fpe
```

Invoke `/first-principles:engineering` or `/first-principles:repo-hardening`, or let Claude load the relevant skill automatically.

## Codex

```sh
codex plugin marketplace add schorsch888/first-principles-engineering-skill
codex plugin add first-principles@fpe
```

Invoke `$first-principles:engineering` or `$first-principles:repo-hardening`, or ask Codex for the matching workflow.

## Development validation

```sh
claude plugin validate .
```

Codex validates `.codex-plugin/plugin.json` and the bundled skill during plugin ingestion.
