# Intervals API Project

A personal training and wellness application built around a data engineering pipeline.

**Status:** early documentation and feasibility review. The application and pipeline have not been implemented.

**Project owner:** Samuel Fernandes. English is the working language for discussions, code, documentation, and development artifacts.

## Purpose

Make training and wellness data easier to understand while learning to build and operate a complete data lifecycle: ingestion, storage, processing, quality checks, analytical modeling, and delivery to an application.

The project uses real personal data from Intervals.icu. Exercises, sets, repetitions, loads, and goals will be entered directly in the application.

## Current direction

| Responsibility | Technology or approach | Status |
| --- | --- | --- |
| Activity and wellness source | Intervals.icu API, receiving data directly from Zepp | Reads verified; unattended wellness refresh still to verify |
| Ingestion and integration | Python | Selected; execution environment open |
| Lakehouse | Delta Lake with bronze, silver, and gold layers | Selected architectural direction |
| Processing | Databricks Free Edition with PySpark/SQL | Conditionally selected, subject to feasibility checks |
| Lake storage | Databricks-managed storage and Unity Catalog volumes | Leading candidate; not yet validated |
| Processing trigger | File arrival | Preferred; Free Edition support not yet verified |
| Application database | PostgreSQL | Selected |
| Database hosting | Neon Free | Candidate |
| Application | Django, usable on desktop and mobile | Selected |
| Application hosting | Vercel Hobby | Candidate |
| Source control | This GitHub repository | Established |

No production deployment, cost measurement, refresh-time target, or final physical data model exists yet. These documents distinguish selected directions from proposals.

## What has been verified

Samuel has verified the following in his own account:

- Historical activities imported from the direct Amazfit/Zepp connection into Intervals.icu.
- Newly recorded activities subsequently appeared in Intervals.icu.
- The activities API returned real activity records with Zepp as their source.
- The wellness API returned records containing sleep and other daily measurements.

These checks do not yet establish a fully unattended pipeline, a measured delivery delay, or compatibility with Databricks Free Edition.

## Documentation

Start with the [documentation guide](README.md).

- [Project brief and scope](project-brief.md)
- [Proposed architecture](architecture.md)
- [Data sources and observations](data-sources.md)
- [Decisions and open questions](decisions.md)
- [Feasibility checks](feasibility.md)
- [Proposed delivery stages](roadmap.md)
- [Contribution and learning workflow](CONTRIBUTING.md)
- [Instructions for AI assistants](AGENTS.md)

## Development status

There are no installation or execution instructions yet because application code, dependencies, and infrastructure have not been created. Add verified instructions as each component becomes runnable.

The next step is a human review of these documents, followed by the feasibility checks that determine whether the proposed free stack can support the project.

## Public portfolio and private data

This repository will explain the architecture, decisions, code, and verification evidence. Real health data, GPS routes, credentials, and database exports must remain private. Public examples should use clearly identified synthetic data.

The application is intended for one personal user. A public demonstration, if created, must use separate synthetic data.

## License

No license has been selected. Record the owner's choice before adding a license file.
