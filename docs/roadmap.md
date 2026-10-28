# Proposed delivery stages

**Status:** proposal for Samuel's review, not a committed schedule.  
**Last updated:** 2026-10-28

**Progress:** Stage 0 completed on 2026-10-28. Stage 1 (platform path) is next, beginning with F03.

These stages describe learning and delivery order. They are not GitHub milestones yet. No deadlines or effort estimates have been approved.

| Stage | Objective | Completion evidence |
| --- | --- | --- |
| 0. Review the foundation | Confirm purpose, scope, responsibilities, and decision ownership | Samuel reviews the brief and corrects the decision register |
| 1. Verify the platform path | Establish a workable ingestion-to-application route within the spending ceiling | Required feasibility checks pass or alternatives are explicitly accepted |
| 2. Define the first useful data product | Choose initial business questions, grains, metric definitions, and source contracts | Human-reviewed definitions with examples and missing-value rules |
| 3. Build one complete data slice | Move a small selected dataset from collection through persisted results | Repeatable collection and processing, observable execution, no duplicate business records on rerun |
| 4. Add dependable operation | Handle edits, retries, backfill, quality failures, and publication consistency | Relevant failure and recovery scenarios demonstrated |
| 5. Deliver the personal application | Show published metrics and record manual workout details | Authenticated desktop/mobile use and persisted manual records |
| 6. Connect manual records to analytics | Include exercise details in selected lakehouse outputs | Changes to manual records propagate according to a documented contract |
| 7. Prepare portfolio evidence | Make the design and execution understandable and reproducible | English documentation, synthetic examples, demonstration, and honest limitations |
| Later. Explore LLM assistance | Assess whether generated interpretation adds useful value | A separate accepted scope, cost estimate, grounding approach, and evaluation |

Stages may overlap where useful. For example, a minimal application deployment belongs in feasibility, while complete screens belong later.

## Learning before automation

For each stage, Samuel should be able to explain:

- What problem this stage solves.
- Why the chosen mechanism fits.
- What the inputs and outputs represent.
- How correctness is checked.
- What failure would look like and how it is detected.

Automation should follow an understood, repeatable process. Add dependencies and services only when they address a demonstrated need.

## What is deliberately not scheduled yet

- Specific screens, metrics, formulas, or final tables.
- A collection interval or freshness service-level target.
- A paid deployment.
- Streaming infrastructure, multi-user support, or a native mobile app.
- LLM implementation.

## First review conversation

Use these prompts to turn the draft into Samuel's plan:

1. What are the first three things you want to learn from your training data?
2. Which of those can the already observed source fields answer?
3. What manual input is worth the effort?
4. What would a successful first end-to-end demonstration look like?
5. Which feasibility uncertainty should be tested first?

## Handoff for the next implementation task

Before changing code, inspect the repository and the current decision register. Select one accepted stage or feasibility check and agree on its observable result. Preserve unrelated behavior, avoid unnecessary dependencies, and keep the task within its defined scope.

Report the files changed, reasoning, checks actually performed, risks, and unresolved decisions. Do not describe the full project as implementation-ready while required feasibility checks or domain decisions remain open.
