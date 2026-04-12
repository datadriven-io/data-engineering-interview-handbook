# The Data Engineering Interview Handbook

> A complete, opinionated, free handbook for passing data engineering interviews at top tech companies.

[![License: CC BY-SA 4.0](https://img.shields.io/badge/License-CC_BY--SA_4.0-lightgrey.svg)](https://creativecommons.org/licenses/by-sa/4.0/)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](#contributing)

If you are preparing for a data engineering interview, you have probably noticed the same problem everyone else has: the field is wide, the rubrics are vague, and most "interview prep" content was written for software engineers, data scientists, or analysts. Almost none of it is calibrated to what actual hiring managers ask data engineers in 2026.

This handbook fixes that. It is a structured, chapter-by-chapter guide to every topic that shows up in a real DE interview loop, with worked examples, study plans, and links to a library of practice problems you can run in your browser.

## Table of contents

1. [How to use this handbook](#how-to-use-this-handbook)
2. [The DE interview loop, explained](#the-de-interview-loop-explained)
3. [Study plans](#study-plans)
4. [Chapter 1: SQL for data engineers](#chapter-1-sql-for-data-engineers)
5. [Chapter 2: Python for data engineers](#chapter-2-python-for-data-engineers)
6. [Chapter 3: Data modeling and schema design](#chapter-3-data-modeling-and-schema-design)
7. [Chapter 4: Pipeline architecture](#chapter-4-pipeline-architecture)
8. [Chapter 5: System design for data engineers](#chapter-5-system-design-for-data-engineers)
9. [Chapter 6: Behavioral and case interviews](#chapter-6-behavioral-and-case-interviews)
10. [Chapter 7: Company specific guides](#chapter-7-company-specific-guides)
11. [Practice environments](#practice-environments)
12. [Resources](#resources)
13. [Contributing](#contributing)

## How to use this handbook

Read sequentially if you are new to interview prep. Jump to the chapter you need if you are revisiting after a year off.

Every chapter follows the same structure:

1. **What interviewers actually test.** Not the textbook definition. The job-relevant skill the question is meant to surface.
2. **Common failure modes.** The mistakes that cause "no hire" votes even when the candidate writes code that runs.
3. **Concept primer.** A short lesson with the minimum theory you need.
4. **Worked examples.** Real interview questions, solved end to end.
5. **Practice set.** A graded list of problems you can run in a browser.

You should be able to read one chapter in an evening and finish the practice set over a weekend.

## The DE interview loop, explained

A typical senior DE loop in 2026 has five rounds:

| Round | What it tests | What you need to prepare |
|---|---|---|
| Recruiter screen | Resume fit, salary band | Resume, story bank |
| SQL screen | Window functions, joins, performance reasoning | Chapter 1 |
| Python / coding | Data manipulation, complexity, edge cases | Chapter 2 |
| Data modeling round | Schema tradeoffs, dimensional vs normalized, SCD | Chapter 3 |
| System design round | End to end pipeline, batch vs stream, cost tradeoffs | Chapters 4 and 5 |
| Behavioral round | Conflict, ambiguity, ownership stories | Chapter 6 |

The two rounds candidates underestimate the most are **schema design** and **pipeline system design**. Both reward depth in tradeoffs, not breadth in tools. We give them the most space in this handbook.

A longer breakdown of the loop, written for 2026 candidates, lives at <https://datadriven.io/data-engineering-interview-prep>.

## Study plans

Pick the plan that matches your timeline.

### 4 week sprint (you have an onsite next month)

| Week | Focus | Daily target |
|---|---|---|
| 1 | SQL drills, joins and window functions | 5 problems per day |
| 2 | Python data manipulation, complexity | 4 problems per day |
| 3 | Data modeling and schema design | 1 schema per day |
| 4 | Pipeline architecture and behavioral stories | 1 case study per day, plus story bank |

### 8 week build (you have two months)

Run the 4 week sprint twice. First pass for breadth, second pass for the patterns you missed. Add a weekly mock interview in week 5 onward.

### 12 week ramp (you are switching into DE from analytics or SWE)

Spend weeks 1 to 4 on the [foundations lessons](https://datadriven.io/learn) for SQL and Python. Weeks 5 to 8 on schema design and pipelines. Weeks 9 to 12 on company specific prep using Chapter 7.

A printable version of the 12 week plan is at <https://datadriven.io/data-engineering-study-plan>.

## Chapter 1: SQL for data engineers

### What interviewers actually test

DE SQL interviews are not the same as analyst SQL interviews. The bar is:

1. Can you write a window function under time pressure without looking up the syntax?
2. Can you reason about query plans, partitioning, and join strategies?
3. Can you find the bug in a query someone else wrote?
4. Can you spot when a question is secretly a data quality question, not a SQL question?

If you can do those four things, you will pass any SQL screen. Everything else (CTEs, COALESCE, CASE, aggregations) is table stakes.

### Concept primer

Read these in order. Each one is a short lesson with runnable examples.

- **Joins.** [Beginner](https://datadriven.io/learn/joins-beginner) -> [Intermediate](https://datadriven.io/learn/joins-intermediate) -> [Advanced](https://datadriven.io/learn/joins-advanced)
- **Aggregating.** [Beginner](https://datadriven.io/learn/aggregating-beginner) -> [Intermediate](https://datadriven.io/learn/aggregating-intermediate) -> [Advanced](https://datadriven.io/learn/aggregating-advanced)
- **Window functions.** [Beginner](https://datadriven.io/learn/window-functions-beginner) -> [Intermediate](https://datadriven.io/learn/window-functions-intermediate) -> [Advanced](https://datadriven.io/learn/window-functions-advanced)
- **Filtering.** [Beginner](https://datadriven.io/learn/filtering-beginner) -> [Intermediate](https://datadriven.io/learn/filtering-intermediate) -> [Advanced](https://datadriven.io/learn/filtering-advanced)
- **Dates and timestamps.** Often the difference between a passing and failing solution. See <https://datadriven.io/sql-tutorial>.

### Worked example: rolling averages

A common SRE flavored question: *"For each service, compute a rolling 7 day average of its uptime."*

What interviewers want to see:

1. You reach for `AVG() OVER (PARTITION BY service ORDER BY day ROWS BETWEEN 6 PRECEDING AND CURRENT ROW)` without hesitating.
2. You ask whether missing days should be zero filled or skipped. (Both are wrong defaults in different contexts.)
3. You handle the boundary case where a service has fewer than 7 days of data.
4. You know that `RANGE BETWEEN INTERVAL '6' DAY PRECEDING AND CURRENT ROW` is the correct version when days can be missing, and `ROWS` is the wrong answer.

The full solved version of this question is at <https://datadriven.io/interview/7_check_rolling_average>.

### Practice set

Start here and work down. Each link drops you into a runnable workbench with the schema preloaded.

| Difficulty | Problem | What it tests |
|---|---|---|
| Easy | [10 Lowest Uptime Services](https://datadriven.io/interview/10_lowest_uptime_services) | TOP N with ties, ORDER BY |
| Easy | [2FA Confirmation Rate](https://datadriven.io/interview/2fa_confirmation_rate) | Conditional aggregation |
| Medium | [30-Day Page View Counts](https://datadriven.io/interview/30_day_page_view_counts) | Date filtering, daily rollups |
| Medium | [7-Day Onboarding Conversion](https://datadriven.io/interview/7_day_onboarding_conversion) | Funnel analysis |
| Medium | [7-Check Rolling Average](https://datadriven.io/interview/7_check_rolling_average) | Window function, ROWS vs RANGE |
| Hard | [Active Users by Month](https://datadriven.io/interview/active_users_by_month) | Cohort logic, dense_rank |
| Hard | [2nd Most Common Content Type](https://datadriven.io/interview/2nd_most_common_content_type) | Tie breaking, rank vs dense_rank |

There are over 850 SQL problems in the full library, sortable by difficulty and topic, at <https://datadriven.io/sql-interview-questions>.

## Chapter 2: Python for data engineers

### What interviewers actually test

DE Python interviews are not LeetCode. They are usually one of three flavors:

1. **Data manipulation.** Take this list of records, return that summary. Tests fluency with dicts, lists, comprehensions, and sometimes pandas.
2. **Algorithmic but practical.** Implement a batcher, a partitioner, a deduper. Tests complexity awareness without obscure tricks.
3. **System scripting.** Parse this log file, retry these failed API calls. Tests defensiveness and error handling.

You will rarely be asked to invert a binary tree.

### Concept primer

- **Foundations.** [Beginner](https://datadriven.io/learn/foundations-beginner) -> [Intermediate](https://datadriven.io/learn/foundations-intermediate) -> [Advanced](https://datadriven.io/learn/foundations-advanced)
- **Collections.** [Beginner](https://datadriven.io/learn/collections-beginner) -> [Intermediate](https://datadriven.io/learn/collections-intermediate) -> [Advanced](https://datadriven.io/learn/collections-advanced)
- **Complexity.** [Beginner](https://datadriven.io/learn/complexity-beginner) -> [Intermediate](https://datadriven.io/learn/complexity-intermediate) -> [Advanced](https://datadriven.io/learn/complexity-advanced)

### Practice set

| Difficulty | Problem | Pattern |
|---|---|---|
| Easy | [Batch Records](https://datadriven.io/interview/batch_records) | Chunking iterables |
| Easy | [Column Sum](https://datadriven.io/interview/column_sum) | Dict aggregation |
| Medium | [Activity Time Ledger](https://datadriven.io/interview/activity_time_ledger) | Interval merging |
| Medium | [Batch Partitioner](https://datadriven.io/interview/batch_partitioner) | Hash bucketing |
| Medium | [Batch With Metadata](https://datadriven.io/interview/batch_with_metadata) | Stateful iteration |
| Hard | [Caesar Shift Check](https://datadriven.io/interview/caesar_shift_check) | String, modular arithmetic |
| Hard | [Character Occurrence Map](https://datadriven.io/interview/character_occurrence_map) | Counting, sorting tradeoffs |

The full Python set (388 problems) is at <https://datadriven.io/python-interview-questions>.

## Chapter 3: Data modeling and schema design

This is the chapter that wins or loses senior loops. Most candidates can write SQL. Very few can defend a schema under pressure.

### What interviewers actually test

1. Can you draw an ERD on a whiteboard in five minutes?
2. Do you know when to denormalize and when not to?
3. Do you know SCD types 0 through 6 and which one to reach for?
4. Can you model time correctly? (Effective dates, transaction time vs valid time, late arriving facts.)
5. Do you understand the difference between a fact, a dimension, and a bridge table?

### Concept primer

The full data modeling track on datadriven.io has 11 lessons:

- [Keys and identity](https://datadriven.io/learn/data-modeling-keys)
- [Data types](https://datadriven.io/learn/data-modeling-data-types)
- [Relationships](https://datadriven.io/learn/data-modeling-relationships)
- [Normalization](https://datadriven.io/learn/data-modeling-normalization)
- [Dimensional modeling](https://datadriven.io/learn/data-modeling-dimensional)
- [Slowly changing dimensions](https://datadriven.io/learn/data-modeling-scd)
- [Event streams](https://datadriven.io/learn/data-modeling-event-streams)
- [Nested data](https://datadriven.io/learn/data-modeling-nested-data)

A condensed version of the field guide lives at <https://datadriven.io/data-modeling>.

### Worked examples

Each of these is a real interview prompt. Open the link, sketch the schema for 15 minutes, then read the solution.

- [A/B Experiment Assignment Schema](https://datadriven.io/interview/a_b_experiment_assignment_schema). Tests SCD type 2, sticky bucketing, and how to record exposure events.
- [Clickstream and Session Schema](https://datadriven.io/interview/clickstream_and_session_schema). Tests sessionization, late events, and how to model user vs visitor identity.
- [Customer Address History](https://datadriven.io/interview/customer_address_history). Classic SCD type 2 question. The traps are around effective date semantics.
- [Insurance Claims Lifecycle](https://datadriven.io/interview/insurance_claims_lifecycle). Tests state machine modeling and how to record status changes without losing history.
- [Loan Management Schema](https://datadriven.io/interview/loan_management_schema). Tests bridge tables, party roles, and how to model many to many relationships with attributes.

The full schema design library has 56 problems and is at <https://datadriven.io/data-modeling-interview-questions>.

## Chapter 4: Pipeline architecture

### What interviewers actually test

By "pipeline architecture" interviewers mean: *given a business problem, design the end to end data flow*. Not "draw a Lambda architecture diagram". The signal they are looking for:

1. Do you ask about volume, latency, freshness, and cost before drawing anything?
2. Do you understand the tradeoffs between batch, micro batch, and streaming?
3. Do you know which storage format to pick and why?
4. Do you handle backfills, replays, and late data?
5. Do you think about failure modes and on call burden?

### Worked case studies

Pick three of these and design them end to end before reading the solution.

- [Ad Simulation Platform Pipeline](https://datadriven.io/interview/ad_simulation_platform_pipeline). Synthetic event generation, low latency feedback loops.
- [AWS Pipeline Auto Scaling for Variable Volume](https://datadriven.io/interview/aws_pipeline_auto_scaling_for_variable_volume). Cost vs throughput tradeoffs.
- [Card Transaction Streaming Pipeline](https://datadriven.io/interview/card_transaction_streaming_pipeline). Exactly once semantics, fraud feedback.
- [Cellular Connectivity and App Log Data Warehouse](https://datadriven.io/interview/cellular_connectivity_and_app_log_data_warehouse). High cardinality dimension explosion.
- [Capital Markets Intraday Risk Pipeline with BCBS 239 Lineage](https://datadriven.io/interview/capital_markets_intraday_risk_pipeline_with_bcbs_239_lineage). Regulatory lineage requirements.
- [Connected Vehicle Telemetry Pipeline with IaC Deployment](https://datadriven.io/interview/connected_vehicle_telemetry_pipeline_with_iac_deployment). High volume, geo partitioning.

The full pipeline architecture library has 120 case studies, browseable at <https://datadriven.io/data-pipeline-interview-questions>.

## Chapter 5: System design for data engineers

System design for data engineers is its own discipline. The DE flavor of system design is **less about request paths and more about data flows**. You are designing pipelines, not microservices.

The companion repo for this chapter is **[system-design-for-data-engineers](https://github.com/system-design-for-data-engineers)**, which contains a curated collection of long form case studies.

### The framework

Every DE system design answer should hit these eight beats in order:

1. **Clarify the problem.** What is the business question? Who reads the output?
2. **Estimate the volume.** Records per second, bytes per record, retention.
3. **Pick a freshness target.** Real time, near real time, hourly, daily.
4. **Choose batch vs stream.** Justify the choice using volume and freshness.
5. **Pick storage.** Lake, warehouse, lakehouse, OLAP store, kv store.
6. **Sketch the topology.** Source, ingest, transform, serve.
7. **Address failure modes.** Backfills, replays, late data, dedup.
8. **Talk about cost and on call.** What is the steady state spend? Who gets paged?

A longer treatment of the framework is at <https://datadriven.io/data-engineering-system-design>.

## Chapter 6: Behavioral and case interviews

The behavioral round is where strong technical candidates lose offers. The fix is simple but rarely done: **prepare a story bank**.

### Story bank template

Build six stories ahead of time, each ~3 minutes long, in the STAR format. Cover these themes:

1. A time you owned an ambiguous problem end to end.
2. A time you disagreed with a stakeholder and changed their mind.
3. A time you broke production and recovered.
4. A time you mentored someone or raised the bar on your team.
5. A time you killed a project that was not worth doing.
6. A time you shipped something fast but rough, and the followup.

Practice them out loud. Then map each story to multiple possible questions.

A list of the 50 most common DE behavioral questions is at <https://datadriven.io/behavioral-interview-questions>.

## Chapter 7: Company specific guides

Each guide covers the actual loop structure, the question style, the leveling rubric, and a curated practice set drawn from past candidate reports.

| Company | Guide |
|---|---|
| Netflix | <https://datadriven.io/companies/netflix/interview> |
| Uber | <https://datadriven.io/companies/uber/interview> |
| Amazon | <https://datadriven.io/companies/amazon/interview> |
| Google | <https://datadriven.io/companies/google/interview> |
| Meta | <https://datadriven.io/companies/meta/interview> |

Resume and salary references for each company live one level up at <https://datadriven.io/companies>.

## Practice environments

You do not need a local setup. Every problem in this handbook runs in a browser sandbox with the schema preloaded:

- SQL workbench: <https://datadriven.io/sql-practice>
- Python workbench: <https://datadriven.io/python-practice>
- Window functions drill: <https://datadriven.io/sql-window-functions-practice>
- Daily challenge (one new problem each day): <https://datadriven.io/data-engineer-interview-questions>

If you prefer local, every problem in the practice sets above includes the schema as a SQL DDL block you can paste into Postgres or DuckDB.

## Resources

### Books worth reading

- *Designing Data Intensive Applications*, Martin Kleppmann. Still the canonical reference for DE system design.
- *The Data Warehouse Toolkit*, Ralph Kimball. The dimensional modeling bible.
- *Fundamentals of Data Engineering*, Joe Reis and Matt Housley. Best modern survey of the field.

### Blogs

- Netflix Tech Blog
- Uber Engineering
- Airbnb Engineering Data Science blog
- Stripe Engineering
- The DataDriven blog at <https://datadriven.io/blog>

### Roadmaps and reference material

- Career roadmap: <https://datadriven.io/data-engineer-roadmap>
- Tooling map: <https://datadriven.io/data-engineering-tools>
- Concept index: <https://datadriven.io/data-engineering-concepts>

## Contributing

This handbook is community maintained. Three ways to help:

1. **Add a worked example.** Open a PR adding a new problem to a practice set with a one paragraph explanation of what it tests.
2. **Fix an error.** Spot a wrong claim, an outdated link, or a confusing explanation? Open an issue or send a PR.
3. **Share a war story.** Each chapter has a `war-stories.md` file. Add yours (anonymized).

Please run `markdownlint` on your changes before opening a PR.

## License

This handbook is released under [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/). You can copy, remix, and republish it commercially as long as you credit the original and share derivative work under the same license.

The linked problem environments and lesson content are hosted at <https://datadriven.io> and used here with permission.
