<h1 align="center">Data Engineering Interview Handbook</h1>

<p align="center">
  Free, structured prep for data engineering interviews. Chapters by round, worked examples, runnable problems.
</p>

<p align="center">
  <a href="https://github.com/datadriven-io/data-engineering-interview-handbook/stargazers"><img src="https://img.shields.io/github/stars/datadriven-io/data-engineering-interview-handbook?style=flat&color=ffd33d" alt="Stars"></a>
  <a href="https://github.com/datadriven-io/data-engineering-interview-handbook/blob/main/LICENSE"><img src="https://img.shields.io/badge/license-CC%20BY--SA%204.0-blue.svg" alt="License"></a>
  <img src="https://img.shields.io/badge/PRs-welcome-brightgreen.svg" alt="PRs welcome">
  <a href="https://datadriven.io"><img src="https://img.shields.io/badge/sandbox-datadriven.io-9333ea.svg" alt="Sandbox"></a>
</p>

<p align="center">
  <a href="#chapters">Chapters</a> ·
  <a href="#study-plans">Study plans</a> ·
  <a href="#companion-repos">Companion repos</a> ·
  <a href="https://datadriven.io">Live sandboxes</a>
</p>

---

Most "interview prep" material was written for software engineers, data scientists, or analysts. This handbook is calibrated for data engineers. Each chapter covers one round of a real DE loop with the specific patterns interviewers test, plus a practice set you can run in a browser at [datadriven.io](https://datadriven.io).

If you have a loop coming up soon, jump to the [study plans](#study-plans). If you want to drill a specific topic, pick a [chapter](#chapters).

## Chapters

| Round | Chapter |
|---|---|
| SQL screen | [1. SQL](#1-sql) |
| Coding | [2. Python](#2-python) |
| Modeling | [3. Data modeling and schema design](#3-data-modeling-and-schema-design) |
| System design | [4. Pipeline architecture](#4-pipeline-architecture) |
| System design | [5. The eight beat framework](#5-the-eight-beat-framework) |
| Behavioral | [6. Behavioral](#6-behavioral) |
| Pre-onsite | [7. Company guides](#7-company-guides) |

## Study plans

| Timeline | Use when | Outline |
|---|---|---|
| **4 week sprint** | Onsite next month | Week 1 SQL, week 2 Python, week 3 modeling, week 4 design and behavioral |
| **8 week build** | Two months out | Run the sprint twice. First pass for breadth, second for the patterns you missed. Add a weekly mock from week 5. |
| **12 week ramp** | Switching from analytics or SWE | Weeks 1 to 4 on [foundation lessons](https://datadriven.io/learn). Weeks 5 to 8 on modeling and pipelines. Weeks 9 to 12 on company prep. |

Printable 12 week version: [datadriven.io/data-engineering-study-plan](https://datadriven.io/data-engineering-study-plan).

## 1. SQL

DE SQL is not analyst SQL. Bar:

1. Write a window function from memory.
2. Reason about query plans, partitioning, and join strategy.
3. Find the bug in someone else's query.
4. Recognize when a SQL question is secretly a data quality question.

Lessons in order: [joins](https://datadriven.io/learn/joins-advanced), [aggregating](https://datadriven.io/learn/aggregating-advanced), [window functions](https://datadriven.io/learn/window-functions-advanced), [filtering](https://datadriven.io/learn/filtering-advanced), [dates](https://datadriven.io/sql-tutorial), [optimization](https://datadriven.io/sql-query-optimization).

| Problem | Difficulty | Tests |
|---|---|---|
| [10 Lowest Uptime Services](https://datadriven.io/interview/10_lowest_uptime_services) | Easy | TOP N with ties |
| [2FA Confirmation Rate](https://datadriven.io/interview/2fa_confirmation_rate) | Easy | Conditional aggregation |
| [30 Day Page View Counts](https://datadriven.io/interview/30_day_page_view_counts) | Medium | Date filtering |
| [7 Check Rolling Average](https://datadriven.io/interview/7_check_rolling_average) | Medium | Rolling window, ROWS vs RANGE |
| [Active Users by Month](https://datadriven.io/interview/active_users_by_month) | Hard | Cohort logic |
| [2nd Most Common Content Type](https://datadriven.io/interview/2nd_most_common_content_type) | Hard | Tie breaking |

Full set: 854 problems at [datadriven.io/sql-interview-questions](https://datadriven.io/sql-interview-questions).

## 2. Python

DE Python is not LeetCode. It is data manipulation: chunking, sessionization, dedup, retries, interval merging, hash partitioning, schema evolution.

Lessons: [foundations](https://datadriven.io/learn/foundations-advanced), [collections](https://datadriven.io/learn/collections-advanced), [complexity](https://datadriven.io/learn/complexity-advanced).

| Problem | Difficulty | Pattern |
|---|---|---|
| [Batch Records](https://datadriven.io/interview/batch_records) | Easy | Chunking iterables |
| [Column Sum](https://datadriven.io/interview/column_sum) | Easy | Dict aggregation |
| [Activity Time Ledger](https://datadriven.io/interview/activity_time_ledger) | Medium | Interval merging |
| [Batch Partitioner](https://datadriven.io/interview/batch_partitioner) | Medium | Hash bucketing |
| [Batch With Metadata](https://datadriven.io/interview/batch_with_metadata) | Medium | Stateful iteration |
| [Caesar Shift Check](https://datadriven.io/interview/caesar_shift_check) | Hard | String transforms |

Full set: 388 problems at [datadriven.io/python-interview-questions](https://datadriven.io/python-interview-questions).

## 3. Data modeling and schema design

Senior loops are won and lost here. Reward goes to candidates who pick the right grain for fact tables, defend an SCD type, and validate the schema with sample queries.

Lessons: [keys](https://datadriven.io/learn/data-modeling-keys), [data types](https://datadriven.io/learn/data-modeling-data-types), [relationships](https://datadriven.io/learn/data-modeling-relationships), [normalization](https://datadriven.io/learn/data-modeling-normalization), [dimensional modeling](https://datadriven.io/learn/data-modeling-dimensional), [SCD](https://datadriven.io/learn/data-modeling-scd), [event streams](https://datadriven.io/learn/data-modeling-event-streams), [nested data](https://datadriven.io/learn/data-modeling-nested-data).

| Problem | Tests |
|---|---|
| [A/B Experiment Assignment Schema](https://datadriven.io/interview/a_b_experiment_assignment_schema) | SCD type 2, sticky bucketing |
| [Customer Address History](https://datadriven.io/interview/customer_address_history) | Effective dates |
| [Insurance Claims Lifecycle](https://datadriven.io/interview/insurance_claims_lifecycle) | State machines |
| [Clickstream and Session Schema](https://datadriven.io/interview/clickstream_and_session_schema) | Sessionization, late events |
| [Loan Management Schema](https://datadriven.io/interview/loan_management_schema) | Bridge tables |
| [Financial Trading Warehouse](https://datadriven.io/interview/financial_trading_warehouse) | Late arriving facts |

Full set: 56 problems at [datadriven.io/data-modeling-interview-questions](https://datadriven.io/data-modeling-interview-questions).

## 4. Pipeline architecture

End to end design questions ("design Netflix viewing history") reward depth in batch vs stream tradeoffs, storage choice, idempotency, late data, and on-call burden.

| Case study | Domain |
|---|---|
| [Card Transaction Streaming Pipeline](https://datadriven.io/interview/card_transaction_streaming_pipeline) | Real time, exactly once |
| [Cellular Connectivity and App Log Data Warehouse](https://datadriven.io/interview/cellular_connectivity_and_app_log_data_warehouse) | High cardinality |
| [Capital Markets Intraday Risk Pipeline](https://datadriven.io/interview/capital_markets_intraday_risk_pipeline_with_bcbs_239_lineage) | Regulatory lineage |
| [Database Replication and Schema Normalization Pipeline](https://datadriven.io/interview/database_replication_and_schema_normalization_pipeline) | CDC |
| [Cost Optimized Clickstream Data Lake](https://datadriven.io/interview/cost_optimized_clickstream_data_lake) | Storage tradeoffs |
| [Connected Vehicle Telemetry Pipeline](https://datadriven.io/interview/connected_vehicle_telemetry_pipeline_with_iac_deployment) | High volume IoT |

Full set: 120 case studies at [datadriven.io/data-pipeline-interview-questions](https://datadriven.io/data-pipeline-interview-questions).

## 5. The eight beat framework

Use this on every system design question. In order:

1. **Clarify** volume, latency, freshness, retention, read pattern.
2. **Estimate** records per second, bytes per record, total per day.
3. **Pick freshness target** (real time, near real time, hourly, daily).
4. **Pick batch vs stream** with arithmetic from beat 2.
5. **Pick storage** (lake, warehouse, lakehouse, OLAP, kv).
6. **Sketch topology** (source, ingest, transform, serve).
7. **Address failure modes** (backfills, replays, late data, dedup).
8. **Talk cost and operations** (monthly spend, on-call burden).

Long form: [datadriven.io/data-engineering-system-design](https://datadriven.io/data-engineering-system-design). Companion repo: [system-design-for-data-engineers](https://github.com/datadriven-io/system-design-for-data-engineers) (120 case studies).

## 6. Behavioral

Build six STAR stories before your loop, three minutes each. Cover these themes:

1. Owned an ambiguous problem end to end.
2. Disagreed with a stakeholder and changed their mind.
3. Broke production and recovered.
4. Mentored or raised the bar.
5. Killed a project that was not worth doing.
6. Shipped fast then cleaned up.

Practice each one out loud. Twice.

50 common DE behavioral questions: [datadriven.io/behavioral-interview-questions](https://datadriven.io/behavioral-interview-questions).

## 7. Company guides

| Company | Guide |
|---|---|
| Netflix | [companies/netflix/interview](https://datadriven.io/companies/netflix/interview) |
| Uber | [companies/uber/interview](https://datadriven.io/companies/uber/interview) |
| Amazon | [companies/amazon/interview](https://datadriven.io/companies/amazon/interview) |
| Google | [companies/google/interview](https://datadriven.io/companies/google/interview) |
| Meta | [companies/meta/interview](https://datadriven.io/companies/meta/interview) |

Full company index: [datadriven.io/companies](https://datadriven.io/companies).

## Companion repos

- [data-engineer-interview-handbook](https://github.com/datadriven-io/data-engineer-interview-handbook). 7 day sprint version of this handbook.
- [data-engineering-interview-questions](https://github.com/datadriven-io/data-engineering-interview-questions). 1418 tagged practice problems.
- [system-design-for-data-engineers](https://github.com/datadriven-io/system-design-for-data-engineers). 120 long form pipeline case studies.
- [data-engineering-cheatsheet](https://github.com/datadriven-io/data-engineering-cheatsheet). One page recall reference for the night before.
- [data-engineer-interview-prep](https://github.com/datadriven-io/data-engineer-interview-prep). 8 week structured practice schedule.
- [awesome-data-engineering-interview](https://github.com/datadriven-io/awesome-data-engineering-interview). Curated list of books, blogs, and tools.
- [awesome-data-engineering-interviews](https://github.com/datadriven-io/awesome-data-engineering-interviews). The DataDriven 75, a focused subset of must-do problems.

## Contributing

PRs welcome. Add a worked example, fix a broken link, or share a war story. Run `markdownlint` before opening a PR.

## License

[CC BY-SA 4.0](LICENSE). Linked sandboxes and lessons hosted at [datadriven.io](https://datadriven.io).
