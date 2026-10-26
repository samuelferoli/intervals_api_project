# Project brief

**Owner:** Samuel Fernandes  
**Status:** initial draft for owner review  
**Last updated:** 2026-10-26

## Problem

Training and wellness data exist across device integrations and interfaces that can be difficult to navigate. The owner wants one useful personal application to review completed training, inspect measurements, record exercise details, and follow progress toward goals.

The learning objective is a complete data engineering lifecycle with real recurring data, clear responsibilities, reproducible source code, and operational evidence.

## Intended outcome

A personal web application, accessible from desktop and mobile, supported by an ingestion and lakehouse pipeline and a PostgreSQL application database.

The pipeline is the main engineering focus. The application provides a useful way to consume its outputs.

## Confirmed requirements

| ID | Requirement |
| --- | --- |
| R01 | Collect activity and wellness data from Intervals.icu repeatedly. |
| R02 | Use a lakehouse approach with bronze, silver, and gold layers. |
| R03 | Prepare dimensional analytical data and training metrics in gold; the final model is still to be designed. |
| R04 | Use PostgreSQL for well-structured application data. |
| R05 | Build the application with Django and make it usable on desktop and mobile. |
| R06 | Allow manual entry of exercises, sets, repetitions, loads, and goals in the application. These details are not expected from Intervals.icu. |
| R07 | Support one personal user and access without relying on the owner's computer remaining online. |
| R08 | Prefer a free stack; any recurring spending should be very small and explicitly understood. No exact paid budget has been approved. |
| R09 | Use English for the project's development and documentation. |
| R10 | Preserve human ownership of reasoning and decisions; AI assists learning, review, and implementation hints. |

Databricks Free Edition is acceptable if ingestion, storage, processing, and delivery are feasible within its restrictions. File arrival is the preferred processing trigger, subject to verification.

## Product capabilities under consideration

- Review completed sessions, training types, and available session measurements.
- Review daily wellness measurements and their history.
- Record exercise details and relate them to sessions.
- Track goals and general progress.
- Provide understandable summaries and, later, improvement suggestions.

The first delivery's exact screens, metrics, and goal types have not been selected.

## Boundaries for the initial delivery

The current direction excludes a multi-user service, a separate native mobile application, and an additional dedicated warehouse service. A responsive web application is the candidate approach.

LLM-generated analysis is a future idea. It is not part of the initial implementation scope. Its eventual role, cost, evaluation, and data access remain undecided.

No claim is made that the personal data volume requires distributed processing. Spark and Delta are selected for learning and demonstration of lakehouse engineering.

## Proposed success criteria

These are review candidates, not approved service-level targets:

- Newly available source data can reach persisted analytical outputs through a repeatable workflow.
- Repeating a collection or processing run does not create duplicate business records.
- Existing records can be updated and historical raw data can be reprocessed.
- Missing measurements remain distinguishable from zero.
- The application can display the most recently published results independently of an active processing job.
- Failures and data freshness are observable.
- Samuel can explain the design, transformations, and operational decisions.
- The public repository demonstrates the work without exposing private data.

Numerical targets for freshness, recovery, spending, retention, and expected usage remain open.

## Questions for Samuel

1. Which three questions should the first version answer?
2. How long after a workout sync is an acceptable delay before it appears in the application?
3. Which manual workout details are essential in the first version?
4. Is any paid monthly amount acceptable, and what is the maximum?
5. What would make the first version useful enough for regular personal use?
