# Feasibility checks

**Status:** proposed checks; none of the platform integration checks below has run.  
**Last updated:** 2026-10-26

## Purpose

Determine whether the candidate free stack can support recurring ingestion and an independently accessible application before committing to a detailed implementation plan.

Existing source API reads are documented in [data sources](data-sources.md). They do not establish connectivity from a hosted collector or Databricks.

## Acceptance evidence

Record the execution date, environment, method, result, limitations, and a sanitized evidence reference for each check. Use passed, failed, blocked, or not run. Record actual observed delays; do not invent a target.

| ID | Check | Evidence needed | Current status |
| --- | --- | --- | --- |
| F01 | Access Intervals.icu from the candidate collector environment | Authenticated activity and wellness reads with secrets kept private; document access restrictions | Not run |
| F02 | Deliver a complete file to managed storage | A synthetic file uploaded and read from the intended Unity Catalog volume using a supported mechanism | Not run |
| F03 | Trigger a job on file arrival | Actual workspace capability verified and a synthetic new file causes a job run; record delay and repeat behavior | Not run |
| F04 | Process files into Delta | A small synthetic batch can be preserved, parsed, and persisted; repeat processing has defined duplicate behavior | Not run |
| F05 | Publish results to hosted PostgreSQL | A synthetic output can be written, read, and safely republished from the intended publisher environment | Not run |
| F06 | Host Django independently | A minimal authenticated application can read/write synthetic records on Vercel and Neon from desktop and mobile without the owner's computer | Not run |
| F07 | Refresh wellness unattended | With normal watch-to-Zepp sync and without visiting the Intervals.icu website, API reads show a newly available wellness measurement | Not run |
| F08 | Observe free-tier resource use | Representative small runs and application access have recorded quota consumption and no unapproved paid resources | Not run |

A proof should be disposable and small. It is not permission to implement the entire application, provision paid infrastructure, or invent production business rules.

## If a check fails

- Identify whether the failure is a configuration issue, a source limitation, or a platform restriction.
- Capture the exact restriction without exposing secrets.
- Compare the smallest alternatives.
- Bring material architecture or budget decisions to Samuel.

Possible alternatives include an external collector, supported API upload, API-triggered jobs, scheduled processing, or an external publisher. These are hypotheses until tested. Do not solve platform restrictions by publishing private data.

## Important boundaries

### File arrival

The source must be collected before a file-arrival trigger can act. A storage trigger does not subscribe to activity creation in Intervals.icu.

Verify whether overwrites are detected and how incomplete uploads are avoided. Prefer an explicit input-completeness approach chosen after examining the upload mechanism.

### Wellness

Prior historical reads succeeded. Ongoing unattended wellness refresh remains uncertain. A forum report indicates website visits affected synchronization for some users. Test current account behavior; do not assume the report proves a current universal limitation.

### Free tiers and availability

A free plan is a resource-limited offering, not a permanent availability guarantee. Measure the likely load before committing to it.

If no acceptable free route exists, document the trade-off and revisit a component or trigger. No paid monthly amount has been approved.

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

- [Free Edition limitations](https://docs.databricks.com/aws/en/getting-started/free-edition-limitations)
- [Working with volume files](https://docs.databricks.com/aws/en/volumes/volume-files)
- [File-arrival triggers](https://docs.databricks.com/aws/en/jobs/file-arrival-triggers)
- [Django on Vercel](https://vercel.com/docs/frameworks/full-stack/django)
- [Neon pricing](https://neon.com/pricing)
- [Wellness synchronization discussion](https://forum.intervals.icu/t/wellness-data-sleep-only-syncs-from-zepp-after-manual-web-login/122754)
