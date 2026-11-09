# Week 13: Data engineering, the bedrock a client audit needs

**Month 4: The Enterprise and Consulting Track (Optional Stretch)** · Untangle the mess before you build on it · 4 lessons · about 12 hours

[← Roadmap](../README.md#the-16-weeks) · [Week 12](week-12.md) · [Week 14 →](week-14.md)

> Weeks 13 to 16 are the optional enterprise track, for Palantir-scale FDE roles: messy client data, cloud at client scale, and the consulting side of the job.

## What you will be able to do

- Advanced SQL beyond joins: window functions, recursive CTEs, and reading an EXPLAIN plan to find why a query scans far more data than it should
- The Medallion architecture: Bronze (raw, immutable), Silver (cleaned, joined, the single source of truth), Gold (business-ready aggregates)
- Star schema versus One Big Table, and when each actually serves a real client dataset better
- Distributed computing basics: how Spark or Ray partition data, and how to recognize data skew and out-of-memory errors when a client dataset exceeds local memory

## You ship this week

> Run a full "data audit" on a real messy public dataset: document the schema problems you find, then rebuild it as a clean Bronze to Silver to Gold pipeline.

Done means:

- [ ] It runs from a clean clone by following your README
- [ ] It has tests, and they pass
- [ ] No secrets in the repository; config comes from environment variables
- [ ] The README says what it does, how to run it, and one thing you would improve next

## Lessons

### 1. Advanced SQL for a data audit - window functions, recursive CTEs and reading EXPLAIN plans

*About 3 hours*

The first week of most enterprise engagements is spent inside someone else's database. The client's "AI project" turns out to depend on a loan table with duplicate rows, a branch hierarchy stored as parent IDs, and a nightly report that takes forty minutes because it reads the whole table to find one month. You cannot fix any of that with joins and `GROUP BY` alone. Window functions let you deduplicate, rank and compare rows without losing detail. Recursive CTEs let you walk hierarchies the client stores as parent pointers. And an `EXPLAIN` plan tells you, before you change anything, why a query reads far more data than it needs to. Weeks 13 to 16 are the optional enterprise track, and this lesson is the SQL toolkit the rest of Week 13 leans on.

Covers: The mental model: SQL runs in a fixed logical order; Window functions on a small payments table.

### 2. The Medallion architecture - Bronze, Silver and Gold, and why the layers exist

*About 2.5 hours*

When a client says "our data is in the lake", they usually mean a folder of CSV exports, a few database dumps and a dashboard nobody trusts. If you build a RAG system or an agent straight on top of that, every wrong answer becomes an argument about whose number is right, and you cannot replay last month's data to prove what changed. The Medallion architecture is a simple, widely used way to impose order: keep the raw data untouched (Bronze), produce one cleaned and validated version of the truth (Silver), and publish business-ready tables built from it (Gold). Databricks popularised the names, Microsoft Fabric uses the same pattern, and many Indian enterprises now describe their data platforms in these terms. You need to know what each layer promises, what belongs where, and how to build one by hand so you can do it without a vendor platform.

Covers: The mental model: each layer is a promise; Why not just clean the data once?; What happens in each step; A complete pipeline in the standard library.

### 3. Star schema versus One Big Table, and choosing for a real client dataset

*About 2.5 hours*

Once Silver is clean, someone has to decide what Gold looks like, and that decision shapes every dashboard, every text-to-SQL agent and every "why does finance's number differ from sales'?" meeting that follows. There are two serious answers. The star schema, from Ralph Kimball's dimensional modelling, splits data into a central table of events (facts) surrounded by tables that describe them (dimensions). One Big Table (OBT) pre-joins everything into a single wide table. Columnar warehouses made OBT cheap and popular; BI tools such as Power BI still work best with stars. A forward deployed engineer is often asked to pick, and to defend the pick to both the client's data team and their business users. This lesson gives you the mechanics and a decision method.

Covers: The mental model: facts are verbs, dimensions are nouns; Fact table; Dimension tables; Both models, side by side, with the trade-offs made visible.

### 4. Distributed data basics - partitions, shuffles, skew and OOM, then the Week 13 data audit

*About 4 hours*

Sooner or later a client hands you data that does not fit on your laptop: three years of UPI transactions, every claim a health insurer has processed, call-centre transcripts for a telecom circle. Pandas raises `MemoryError`, or the kernel simply dies. The usual answer is a distributed engine such as Apache Spark or Ray, often already running in the client's Databricks, EMR, Dataproc or Fabric workspace. These engines do not make problems disappear; they turn one big problem into many small ones and then hit trouble when the pieces are uneven. One hot key (one giant merchant, one busy hospital, one default value like `"UNKNOWN"`) can make a 200-task job wait on a single task for an hour and then fail with an out-of-memory error. This lesson explains how partitioning works, why skew and OOM happen, how to read the symptoms, and then plans the Week 13 deliverable.

Covers: The mental model: split, work locally, shuffle, work locally again; Data skew: when one partition gets most of the rows.

## Free resources

Primary sources used in this week's lessons: official docs, papers and engineering blogs.

- [SQLite: The WITH clause and recursive common table expressions](https://www.sqlite.org/lang_with.html)
- [SQLite: EXPLAIN QUERY PLAN](https://www.sqlite.org/eqp.html)
- [PostgreSQL (current release): Using EXPLAIN](https://www.postgresql.org/docs/current/using-explain.html)
- [PostgreSQL tutorial: Window functions](https://www.postgresql.org/docs/current/tutorial-window.html)
- [Databricks: What is the medallion lakehouse architecture?](https://docs.databricks.com/aws/en/lakehouse/medallion)
- [Microsoft Fabric: Implement medallion lakehouse architecture](https://learn.microsoft.com/en-us/fabric/onelake/onelake-medallion-lakehouse-architecture)
- [Delta Lake: Table deletes, updates and merges](https://docs.delta.io/delta-update/)
- [NYC TLC Trip Record Data (a good messy dataset for practice)](https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page)
- [Kimball Group: The four-step dimensional design process](https://www.kimballgroup.com/data-warehouse-business-intelligence-resources/kimball-techniques/dimensional-modeling-techniques/four-4-step-design-process/)
- [Microsoft Learn: Understand star schema and the importance for Power BI](https://learn.microsoft.com/en-us/power-bi/guidance/star-schema)
- [BigQuery: Use nested and repeated fields](https://docs.cloud.google.com/bigquery/docs/best-practices-performance-nested)
- [Apache Spark: Performance Tuning (Spark SQL, adaptive query execution and skew joins)](https://spark.apache.org/docs/latest/sql-performance-tuning.html)
- [Ray Data internals: blocks, streaming execution, shuffles and memory](https://docs.ray.io/en/latest/data/data-internals.html)

## Check yourself

Answer out loud before opening each answer.

<details><summary>Why does `SELECT *, ROW_NUMBER() OVER (...) AS rn FROM t WHERE rn = 1` fail, and what is the fix?</summary>

`WHERE` is evaluated before window functions, so `rn` does not exist yet at that point. Compute the window in a CTE or subquery and filter on `rn` in the outer query.

</details>

<details><summary>Two payments on the same date: one query uses `SUM(x) OVER (ORDER BY day)` and another `SUM(x) OVER (ORDER BY day ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW)`. How do the results differ?</summary>

The first uses the default `RANGE` frame, so both same-day rows are peers and both show the total including both payments. The second counts physical rows, so the first of the two shows a smaller running total than the second.

</details>

<details><summary>Why must Bronze be immutable and append-only?</summary>

So that Silver and Gold can always be rebuilt from it when a cleaning rule turns out to be wrong or a requirement changes. If Bronze is edited or overwritten, the original data is lost and mistakes become permanent.

</details>

<details><summary>A late correction for a January record arrives in March. What should happen in each layer?</summary>

Bronze appends the correction as a new row with March load metadata. Silver upserts it, replacing the January record's values for that business key. Gold aggregates that include January are rebuilt or updated.

</details>

<details><summary>What does "declare the grain" mean, and why is it the most important step?</summary>

It means stating exactly what one row of the fact table represents, such as one loan disbursement. Every measure and dimension must be true at that grain; mixing grains causes double-counting that is very hard to spot.

</details>

<details><summary>A customer moves from Pune to Bengaluru. Under SCD Type 1 and Type 2, what happens to a report of last year's sales by city?</summary>

Under Type 1 the city is overwritten, so last year's sales move to Bengaluru. Under Type 2 a new dimension row is added for the new city, old facts keep pointing at the Pune version, and last year's report stays unchanged.

</details>

<details><summary>Why does a `groupBy` cause a shuffle while a `filter` does not?</summary>

A filter needs only the rows already in each partition. A `groupBy` needs all rows with the same key in one place, so rows must be re-distributed across the cluster by key.

</details>

<details><summary>A stage has 200 tasks; 199 finish in 30 seconds and one runs for 40 minutes. What do you check first, and why will more executors not help?</summary>

Check the task's input or shuffle read size against the median and the row counts per key: it is almost certainly skew. The oversized key is processed by one task regardless of cluster size, so extra executors sit idle.

</details>

---

**Learn Week 13 hands-on** with worked code, practice problems and an AI tutor that knows which step you are on: [Zero to FDE](https://zero-to-fde-90-days.site/forward-deployed-engineer-program?utm_source=github&utm_medium=referral&utm_campaign=roadmap_repo&utm_content=week13). Week 1 is free.
