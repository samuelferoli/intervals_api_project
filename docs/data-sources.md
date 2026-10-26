# Data sources and observations

**Status:** evidence summary, not a final data contract.  
**Last updated:** 2026-10-26

## 1. Intervals.icu

The owner records activities with an Amazfit Bip U Pro. Zepp is connected directly to Intervals.icu for activity and wellness downloads. Zepp can continue publishing separately to Strava.

The project's demonstrated activity source is Zepp through Intervals.icu. Do not assume Strava-sourced activities have the same API availability.

### Evidence reported by Samuel

| Check | Date | Result | Limit |
| --- | --- | --- | --- |
| Import historical Zepp activities | 2026-10-21 | Activities appeared in Intervals.icu | Manual historical import |
| Read activities API | 2026-10-21 | Non-empty records with source ZEPP | Sample date range only |
| Read wellness API | 2026-10-21 | Daily records included populated sleep and other fields | Some days and fields were null |
| Observe newly recorded activities | Reported 2026-10-26 | New activities appeared in Intervals.icu | No measured delay or unattended collector test |

These observations support source feasibility but do not prove a complete automated ingestion system.

### Endpoints already exercised

| Purpose | Method | Path | Parameters |
| --- | --- | --- | --- |
| List activities | GET | /api/v1/athlete/0/activities | oldest, newest |
| List wellness records | GET | /api/v1/athlete/0/wellness | oldest, newest |

The host is https://intervals.icu. With personal API-key authentication, athlete 0 refers to the key owner. The observed authentication method is HTTP Basic with the literal username API_KEY and the personal key as password.

Keep the key private. No actual key or athlete identifier is needed in this document.

### Fields observed in sample responses

| Dataset | Examples | Interpretation boundary |
| --- | --- | --- |
| Activities | id, type, start_date, start_date_local, elapsed_time, moving_time | Preserve original time fields; choose canonical time rules later |
| Activities | average_heartrate, max_heartrate, calories, source, device_name | Measurements and source metadata; availability depends on activity |
| Activities | created, icu_sync_date | Not automatically equivalent to the original event time or every source update |
| Activities | stream_types | Advertises available streams; stream retrieval itself has not been tested |
| Wellness | id, sleepSecs, sleepScore, sleepQuality, steps, restingHR | Observed daily measurements; field definitions require review |
| Wellness | hrv, hrvSDNN | Present but null in the sample; do not promise populated HRV |

A null means the value is absent in the returned record. It does not, by itself, explain whether the cause is no measurement, source support, synchronization, or another issue. Keep null distinct from zero.

No evidence establishes availability of detailed sleep stages, exercise-level sets, repetitions, or loads from this integration. Fields must be validated before they become product requirements.

### Contract questions

- What are the units and exact meanings of each selected field?
- What distinguishes a raw device measurement from a metric calculated by Intervals.icu?
- How are corrected and deleted activities represented?
- Which timestamps can reliably identify updates?
- Which pagination, rate limits, retry guidance, and range limits apply?
- Which date owns an overnight sleep record?
- Are source identifiers stable through reimports?
- Does wellness refresh continue without opening the Intervals.icu website?

Do not infer stable contracts from one sample response.

## 2. Manual application records

The owner will enter exercises, sets, repetitions, loads, and goals in Django. PostgreSQL is the source of truth for these records.

The schema, units, validation, session links, edit history, and deletion behavior remain to be designed by Samuel. If these records feed lakehouse metrics, their ingestion and update behavior require a separate contract.

## Data modeling prompts

Candidate analytical grains include one row per activity and one row per athlete-day. They are proposals, not approved tables.

Joining daily wellness to multiple activities can duplicate daily measurements. Define each grain and aggregation rule before calculating combined metrics.

## Evidence handling

Keep full personal payloads outside the public repository. Create synthetic fixtures after the necessary field subset is chosen. Public verification notes should contain status, methods, and sanitized findings rather than real health values or routes.

## References

- [Intervals.icu API guide](https://forum.intervals.icu/t/api-access-to-intervals-icu/609)
- [API integration cookbook](https://forum.intervals.icu/t/intervals-icu-api-integration-cookbook/80090)
- [Zepp integration announcement](https://forum.intervals.icu/t/amazfit-zepp-support-available/107652/1)
- [Reported unattended wellness refresh limitation](https://forum.intervals.icu/t/wellness-data-sleep-only-syncs-from-zepp-after-manual-web-login/122754)

The wellness discussion identifies a risk to test in the owner's current account, not proof that the limitation still affects every account.
