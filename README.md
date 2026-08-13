# First-Principles Engineering

An evidence-led engineering skill for reframing requirements, architecture decisions, bugs, and remediation plans before implementation.

The repository contains one shared `SKILL.md` and native plugin metadata for both Claude Code and Codex.

## Claude Code

```text
/plugin marketplace add schorsch888/first-principles-engineering-skill
/plugin install first-principles-engineering-skill@first-principles-engineering-skill
```

Invoke it with `/first-principles-engineering-skill:first-principles-engineering` or let Claude load it when the request matches its description.

## Codex

```sh
codex plugin marketplace add schorsch888/first-principles-engineering-skill
codex plugin add first-principles-engineering-skill@first-principles-engineering-skill
```

Invoke the installed skill explicitly or ask Codex for first-principles analysis.

## Development validation

```sh
claude plugin validate .
```

Codex validates `.codex-plugin/plugin.json` and the bundled skill during plugin ingestion.
