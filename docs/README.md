# Documentation guide

These documents capture the early project discussion as of **2026-10-26**, updated on **2026-10-28** after the Phase 0 review (Databricks removed; Azure, PySpark, and a webhook trigger proposed). They are a starting point for Samuel's review, not a completed implementation specification.

## Reading order

| Order | Document | Purpose |
| --- | --- | --- |
| 1 | [Project brief](project-brief.md) | Explain the problem, confirmed requirements, boundaries, and intended outcomes. |
| 2 | [Architecture](architecture.md) | Explain component responsibilities and the proposed data flow. |
| 3 | [Data sources](data-sources.md) | Separate observed source capabilities from assumptions. |
| 4 | [Decisions](decisions.md) | Track selected directions, conditional choices, and unresolved questions. |
| 5 | [Feasibility](feasibility.md) | Define the evidence needed before committing to the Azure-based stack. |
| 6 | [Roadmap](roadmap.md) | Suggest delivery stages and completion evidence without fixing dates. |

Read [the project overview](project-overview.md), [CONTRIBUTING](CONTRIBUTING.md), and [AGENTS](AGENTS.md) for the development and learning workflow.

## Status vocabulary

- **Confirmed requirement:** explicitly requested by Samuel.
- **Selected direction:** accepted in discussion; details may remain open.
- **Conditional:** acceptable only if named checks pass.
- **Proposed:** a suggestion awaiting Samuel's decision.
- **Observed:** behavior reported or demonstrated in the account; not a universal guarantee.
- **Open:** unresolved.
- **Deferred:** deliberately outside the initial delivery.

## Review boundaries

The documents do not choose a collection frequency, exact metric formulas, final tables, authentication mechanism, or deployment configuration. The spending ceiling (20 BRL per month) is set. They do not claim that webhook registration on a personal Intervals.icu account, or any Azure integration, has been tested.

A feature may be part of the product vision while its delivery stage remains open. Provider features and pricing are time-sensitive; consult the linked official documentation again before implementation.

## How to review

Start with the project brief and decision log. Correct anything that misrepresents your intent. Then use the feasibility checks to decide whether the proposed services can work together before expanding the implementation plan.
