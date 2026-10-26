# Decisions and open questions

**Owner:** Samuel Fernandes  
**Last updated:** 2026-10-26

An accepted direction is not evidence that an integration has passed. Do not mark a candidate accepted merely because its documentation was merged.

## Decision register

| ID | Topic | Status | Direction and rationale |
| --- | --- | --- | --- |
| D01 | Ownership and AI assistance | Accepted | Samuel reasons about and owns the design. AI supports study, feedback, review, and requested assistance. |
| D02 | Working language | Accepted | Use English throughout development for practice and international readability. |
| D03 | Product audience | Accepted | One personal user; desktop and mobile access through a web application. |
| D04 | External data source | Accepted | Intervals.icu receiving Zepp directly; activity and wellness sample reads succeeded. |
| D05 | Application-entered data | Accepted | Exercises, sets, repetitions, loads, and goals are recorded directly in the app. |
| D06 | Lakehouse direction | Accepted | Delta Lake and medallion, with dimensional analytical outputs in gold. Physical models are open. |
| D07 | Application technologies | Accepted | Django and PostgreSQL match the owner's skills and application needs. |
| D08 | Databricks edition | Conditional | Free Edition is acceptable if the ingestion, storage, processing, and publication checks pass. |
| D09 | Primary lake storage | Proposed | Use Databricks-managed storage and a managed volume for raw files. This simplifies the candidate free setup; compatibility remains untested. |
| D10 | Processing trigger | Preferred, conditional | File arrival if available and suitable in the actual workspace. An API-triggered or scheduled job is a fallback candidate. |
| D11 | Hosting | Proposed | Vercel Hobby for Django and Neon Free for PostgreSQL, subject to a deployment and quota check. |
| D12 | Dedicated warehouse service | Proposed exclusion | Keep analytical data in Delta and publish the needed serving subset to PostgreSQL; review only if a concrete need emerges. |
| D13 | LLM integration | Deferred | Consider grounded summaries or recommendations after the underlying data and metric definitions are reliable. |

## Open questions

| ID | Question | Why it matters | Owner |
| --- | --- | --- | --- |
| Q01 | Which business questions and metrics belong in the first release? | Defines the first useful data products and application scope | Samuel |
| Q02 | What end-to-end update delay is acceptable? | Determines collection frequency, trigger design, and resource use | Samuel |
| Q03 | Where does the recurring collector run? | Determines unattended collection and access to storage | Samuel, after feasibility evidence |
| Q04 | What should happen if file arrival is unavailable? | Determines whether to change the trigger or revisit the platform | Samuel |
| Q05 | How are data published if the Free Edition cannot reach PostgreSQL directly? | Determines publisher location and integration method | Samuel, after feasibility evidence |
| Q06 | What paid monthly maximum, if any, is acceptable? | Prevents unsupported cost assumptions | Samuel |
| Q07 | How will the single user authenticate? | Protects private data in the hosted application | Samuel |
| Q08 | What are the facts, dimensions, keys, units, and metric formulas? | Prevents inconsistent analysis and accidental duplication | Samuel |
| Q09 | How are application records linked to imported sessions? | Connects manually recorded exercises with source activities | Samuel |
| Q10 | What retention, backup, deletion, and recovery behavior is needed? | Defines data lifecycle and recovery expectations | Samuel |
| Q11 | Which license should the repository use? | Establishes reuse terms | Samuel |

## Recording a substantial decision

When a choice needs more explanation, add a short record with:

- Date and owner.
- Status: proposed, accepted, rejected, or superseded.
- Problem and constraints.
- Options considered.
- Decision and rationale in Samuel's own words.
- Consequences and evidence.
- A link to any decision it replaces.

Separate larger architecture decision records can be introduced when useful. The register is sufficient for the current stage.
