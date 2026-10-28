# Feasibility checks

**Status:** proposed checks; none of the platform integration checks below has run.  
**Last updated:** 2026-10-28

## Purpose

Determine whether the candidate Azure-based stack can support event-driven ingestion and an independently accessible application within the spending ceiling (D16) before committing to a detailed implementation plan.

Existing source API reads are documented in [data sources](data-sources.md). They do not establish connectivity from a hosted collector or Azure.

## Acceptance evidence

Record the execution date, environment, method, result, limitations, and a sanitized evidence reference for each check. Use passed, failed, blocked, or not run. Record actual observed delays; do not invent a target.

| ID | Check | Evidence needed | Current status |
| --- | --- | --- | --- |
| F01 | Access Intervals.icu from the candidate Azure environment | Authenticated activity and wellness reads from an Azure Function with secrets kept private; document access restrictions | Not run |
| F02 | Deliver a complete file to ADLS Gen2 | A synthetic file written by the Azure Function and read back from the intended container using a supported mechanism; no incomplete file is visible to readers | Not run |
| F03 | Register and receive an Intervals.icu webhook on a personal account | OAuth app approved and authorized for Samuel's account; an `ACTIVITY_UPLOADED` and a `WELLNESS_UPDATED` event for a real or test activity reaches an HTTPS endpoint; secret verification, 2xx handling, retry, and duplicate delivery behavior recorded; observed delay recorded | Not run |
| F04 | Run PySpark and Delta on ADLS in an on-demand job | A container job starts from the receiving function (or Event Grid), reads a small synthetic batch from ADLS, writes Delta tables, and exits; repeat processing has defined duplicate behavior; start-up and run time recorded | Not run |
| F05 | Publish results to hosted PostgreSQL | A synthetic output can be written, read, and safely republished from the processing job (for example over JDBC to Neon) | Not run |
| F06 | Host Django independently | A minimal authenticated application can read/write synthetic records on Vercel and Neon from desktop and mobile without the owner's computer | Not run |
| F07 | Refresh wellness unattended | With normal watch-to-Zepp sync and without visiting the Intervals.icu website, API reads show a newly available wellness measurement | Not run |
| F08 | Observe resource use and cost against the ceiling | Current Azure pricing and free grants checked for Storage, Functions, and Container Apps jobs; a hard spending cap or equivalent control is in place; representative small runs have recorded consumption and cost below 20 BRL per month (D16) | Not run |
| F09 | Fallback trigger (only if F03 fails) | A timer-triggered poll or GitHub Actions workflow collects new activities and starts the same processing path; observed delay recorded | Not run |

A proof should be disposable and small. It is not permission to implement the entire application, provision paid infrastructure, or invent production business rules.

## If a check fails

- Identify whether the failure is a configuration issue, a source limitation, or a platform restriction.
- Capture the exact restriction without exposing secrets.
- Compare the smallest alternatives.
- Bring material architecture or budget decisions to Samuel.

Possible alternatives include scheduled polling, GitHub Actions, an Event Grid trigger on blob creation, or an external publisher. These are hypotheses until tested. Do not solve platform restrictions by publishing private data.

## Important boundaries

### Webhooks and delivery

The Intervals.icu OAuth application form states that webhooks require an OAuth app; a personal API key cannot receive them. Applications are reviewed manually. The form requires a name, description, website, privacy policy, platforms, and categories. A pending app cannot complete the OAuth flow, so webhook delivery to Samuel's own account depends on approval. Webhook URLs (HTTPS only), an authorization header, and event types are configured on the app. Documented behavior to verify rather than assume: activity webhooks are not delivered for Strava activities; a non-2xx response causes a retry; duplicates can occur; some events (for example `ACTIVITY_ANALYZED`) are sent after a delay of about 60 seconds.

The pipeline starts when Intervals.icu has the activity. The delay before that (watch to Zepp app to Intervals.icu) is outside its control and should be observed, not targeted.

The receiving endpoint should acknowledge quickly, write the payload as a complete file, and leave processing to the job. Verify whether overwrites are detected and how incomplete writes are avoided.

### Wellness

Prior historical reads succeeded. Wellness uses the `WELLNESS_UPDATED` webhook plus a safety-net poll (Q15). The webhook fires only when Intervals.icu receives new data, so the synchronization risk below still applies. Ongoing unattended wellness refresh remains uncertain. A forum report indicates website visits affected synchronization for some users. Test current account behavior; do not assume the report proves a current universal limitation.

### Cost and availability

Azure services bill by usage, and some offer free monthly grants. Check current prices and grants before enabling anything (F08); they change. The approved ceiling is 20 BRL per month (D16). A budget alert alone is not a spending cap.

If the stack cannot stay within the ceiling, document the trade-off and bring the choice to Samuel.

## Completion rule

The candidate architecture can be accepted when its required integration path has passed and Samuel has decided how to handle any exceptions. A failed preferred trigger does not automatically invalidate the whole project, but its replacement requires a recorded decision.

Before detailed implementation, choose the initial business questions, refresh target, hosting approach, authentication approach, and cost boundary. See the [decision log](decisions.md).

## Suggested evidence entry

| Field | Value |
| --- | --- |
| Check ID | |
| Date and environment | |
| Method | |
| Expected behavior | |
| Observed behavior | |
| Status | |
| Sanitized evidence reference | |
| Limitations and next decision | |

## References

- [Intervals.icu API Integration Cookbook (webhooks)](https://forum.intervals.icu/t/intervals-icu-api-integration-cookbook/80090)
- [Azure Data Lake Storage Gen2 introduction](https://learn.microsoft.com/en-us/azure/storage/blobs/data-lake-storage-introduction)
- [Azure Container Apps jobs](https://learn.microsoft.com/en-us/azure/container-apps/jobs)
- [Azure Blob Storage events](https://learn.microsoft.com/en-us/azure/storage/blobs/storage-blob-event-overview)
- [Django on Vercel](https://vercel.com/docs/frameworks/full-stack/django)
- [Neon pricing](https://neon.com/pricing)
- [Wellness synchronization discussion](https://forum.intervals.icu/t/wellness-data-sleep-only-syncs-from-zepp-after-manual-web-login/122754)
