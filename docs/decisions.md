# Decisions and open questions

**Owner:** Samuel Fernandes  
**Last updated:** 2026-10-28

An accepted direction is not evidence that an integration has passed. Do not mark a candidate accepted merely because its documentation was merged.

Samuel reviewed and confirmed D01-D07 on 2026-10-28 (Phase 0).

## Decision register

| ID | Topic | Status | Direction and rationale |
| --- | --- | --- | --- |
| D01 | Ownership and AI assistance | Accepted | Samuel reasons about and owns the design. AI supports study, feedback, review, and requested assistance. |
| D02 | Working language | Accepted | Use English throughout development for practice and international readability. |
| D03 | Product audience | Accepted | One personal user; desktop and mobile access through a web application. |
| D04 | External data source | Accepted | Intervals.icu receiving Zepp directly; activity and wellness sample reads succeeded. |
| D05 | Application-entered data | Accepted | Exercises, sets, repetitions, loads, and goals are recorded directly in the app. |
| D06 | Lakehouse direction | Accepted | Delta Lake and medallion on ADLS Gen2, processed with PySpark, with dimensional analytical outputs in gold. Physical models are open. |
| D07 | Application technologies | Accepted | Django and PostgreSQL match the owner's skills and application needs. |
| D08 | Databricks edition | Superseded (2026-10-28) | Samuel removed Databricks from the stack. The Free Edition checks (storage, file-arrival trigger, PostgreSQL reachability) were never run and are replaced by the Azure-based checks. Replaced by D09, D10, and D14. |
| D09 | Primary lake storage | Accepted | ADLS Gen2 on Azure. Chosen by Samuel for Azure experience and expected low, usage-based cost. Access and cost remain to be confirmed in F02 and F08. |
| D10 | Processing trigger | Conditional | Webhook-driven: an Intervals.icu `ACTIVITY_UPLOADED` event reaches an HTTPS endpoint and starts the pipeline. Depends on F03 (webhook registration on a personal account). Fallback candidates: scheduled API polling or GitHub Actions; choose with Samuel if F03 fails or cost is too high. |
| D11 | Hosting | Proposed | Vercel Hobby for Django and Neon Free for PostgreSQL, subject to a deployment and quota check. |
| D12 | Dedicated warehouse service | Proposed exclusion | Keep analytical data in Delta and publish the needed serving subset to PostgreSQL; review only if a concrete need emerges. |
| D13 | LLM integration | Deferred | Consider grounded summaries or recommendations after the underlying data and metric definitions are reliable. |
| D14 | Processing engine | Accepted | PySpark and Delta Lake for bronze, silver, and gold. Samuel prefers Spark over lighter engines (for example DuckDB, Polars, or delta-rs) as a learning goal. Both libraries are open source with no licence fee; only the compute that runs them is billed. |
| D15 | Execution environment | Proposed | An Azure Function receives and verifies webhooks and writes raw payloads to ADLS. PySpark runs in local mode in an on-demand Azure Container Apps job, which also publishes to PostgreSQL. Event Grid on blob creation is an alternative job trigger. Untested. Managed Spark platforms (Databricks, Synapse, Fabric) are not selected; their cost against D16 has not been evaluated. |
| D16 | Spending ceiling | Accepted | Up to 20 BRL per month, stated by Samuel on 2026-10-28. A hard cap or equivalent control must be in place before enabling paid resources (see F08). |

## Open questions

| ID | Question | Why it matters | Owner |
| --- | --- | --- | --- |
| Q01 | Topics chosen on 2026-10-28: sleep analysis, run metrics and measures, and gym frequency. Which concrete questions and metrics belong in the first release? | Defines the first useful data products and application scope | Samuel |
| Q03 | Where do the receiving endpoint and the processing job run? Proposed in D15. | Determines unattended operation and access to storage | Samuel, after F01-F04 |
| Q04 | What happens if webhook registration is unavailable on a personal account? | Determines the fallback trigger (polling or GitHub Actions) | Samuel, after F03 |
| Q05 | Can the processing job reach hosted PostgreSQL directly? Proposed: JDBC from the job (D15). | Determines publisher location and integration method | Samuel, after F05 |
| Q07 | How will the single user authenticate? | Protects private data in the hosted application | Samuel |
| Q08 | What are the facts, dimensions, keys, units, and metric formulas? | Prevents inconsistent analysis and accidental duplication | Samuel |
| Q09 | How are application records linked to imported sessions? | Connects manually recorded exercises with source activities | Samuel |
| Q10 | What retention, backup, deletion, and recovery behavior is needed? | Defines data lifecycle and recovery expectations | Samuel |
| Q11 | Which license should the repository use? | Establishes reuse terms | Samuel |
| Q15 | How often is wellness polled (batch schedule)? | Determines sleep-analysis freshness and resource use; relates to F07 | Samuel, as the project advances |
| Q16 | Are sleep stages or other sleep fields beyond duration, score, and quality available and needed? | Sleep analysis may need more than the fields Samuel expects to be reliable | Samuel, after inspecting sample wellness records |

## Resolved questions

| ID | Question | Answer | Date |
| --- | --- | --- | --- |
| Q02 | What end-to-end update delay is acceptable? | A few minutes after the activity is available in Intervals.icu is acceptable. No numeric target is set. Delay before the activity reaches Intervals.icu (watch to Zepp app to Intervals.icu) is outside the pipeline's control. | 2026-10-28 |
| Q06 | What paid monthly maximum is acceptable? | Up to 20 BRL per month. Recorded as D16. | 2026-10-28 |
| Q12 | Do gym sessions come from the watch or only from manual records? | Gym sessions come from the watch as Intervals.icu activities. The specific exercises and sets within a session are entered manually in the app (R06, D05). The activity type that identifies a gym session still needs to be confirmed in sample data. | 2026-10-28 |
| Q13 | Which sleep fields are reliable? | Samuel reports that resting heart rate, sleep score, sleep duration, and sleep quality are certain to be present. Sleep stages are not established; see Q16. Field names and units still need validation against sample payloads. | 2026-10-28 |
| Q14 | How and how often is wellness data collected? | In batches, with polling, because no wellness webhook is documented. The frequency is deferred (Q15). | 2026-10-28 |

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
