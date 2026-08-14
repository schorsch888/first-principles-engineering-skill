# Cross-forge labels

Apply exactly one label from each required dimension. The same strings work on GitHub and GitLab; GitLab may additionally enforce them as scoped labels when supported.

## Review effort

| Canonical label | Meaning | Accepted existing alias |
| --- | --- | --- |
| `review-effort::1` | Isolated or mechanical; one obvious review path | `Review effort 1/5` |
| `review-effort::2` | Localized behavior; limited context needed | `Review effort 2/5` |
| `review-effort::3` | Cross-module or domain knowledge needed | `Review effort 3/5` |
| `review-effort::4` | Multi-system, schema, authorization, or operational review | `Review effort 4/5` |
| `review-effort::5` | Architectural, security/privacy, or release-critical review | `Review effort 5/5` |

Do not calculate effort from line count alone. Split effort-5 work unless it cannot remain correct or deployable when divided.

## Risk

| Canonical label | Meaning |
| --- | --- |
| `risk::low` | Mechanical/docs-only or behaviorally inert; trivial rollback |
| `risk::medium` | Localized behavior/configuration change with contained impact and easy rollback |
| `risk::high` | Public contract, auth, migration, deployment, cross-service, or coordinated rollback impact |
| `risk::critical` | Irreversible/destructive data, security/privacy boundary, emergency, or broad release impact |

High and critical risk require named owners, observable rollout signals, and a tested or explicitly reviewed rollback/roll-forward plan.

## Keep labels minimal

- Allow existing `area::*` or component labels when they improve routing.
- Keep change type in the title/commit convention instead of duplicating it as a label.
- Keep priority on the linked issue/work item, not the review request.
- Use forge review/CI state instead of workflow labels such as ready, review, or blocked.
- Never create, rename, or delete labels during ordinary submission. Bootstrap canonical labels only when repository configuration is explicitly requested.
