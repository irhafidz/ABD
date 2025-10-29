# Week 10 – Database Tuning

## 1. Introduction
- **1.1 What is Database Performance?**
- **1.2 What is Database Tuning?**
- **1.3 Why Database Tuning is Needed**

## 2. Performance Problems in the Real World
- **2.1 Common Bottlenecks in Industry**
- **2.2 Case: Small vs Large Company Issues**
- **2.3 Example: Slow Query in UMKM Database**

## 3. Core Concepts of Database Tuning
- **3.1 Overview of Tuning Areas**
  - Query Tuning  
  - Schema Tuning  
  - Index Tuning  
  - Memory / Configuration Tuning  
  - Application-Level Tuning  
- **3.2 How Tuning Improves Performance**

## 4. Indexing – The Heart of Tuning
- **4.1 What is an Index?**
- **4.2 How Index Works (B-Tree, Hash)**
- **4.3 SQL Example – `CREATE INDEX`**
- **4.4 Comparing Query Time (With vs Without Index)**
- **4.5 Using `EXPLAIN` and `EXPLAIN ANALYZE`**
  - 4.5.1 EXPLAIN Basics  
  - 4.5.2 EXPLAIN ANALYZE (PostgreSQL Doc §14.1)  
  - 4.5.3 Common Caveats  
- **4.6 Measuring Query Performance (Tiger Data)**

## 5. Tools and Techniques for Performance Analysis
- **5.1 Statistics Used by the Planner (PostgreSQL Doc §14.2)**
  - 5.1.1 Single-Column Statistics  
  - 5.1.2 Extended Statistics  
- **5.2 Controlling the Planner (JOIN Clauses)**
- **5.3 Monitoring Tools**
  - EXPLAIN / EXPLAIN ANALYZE  
  - `pg_stat_activity` / Slow Query Log  
  - VACUUM / ANALYZE  
  - pgBadger / Percona Toolkit  
- **5.4 Populating and Bulk Load Tips (PostgreSQL Doc §14.4)**
  - Disable Autocommit  
  - Use `COPY` for Bulk Load  
  - Remove Indexes Before Bulk Insert  
  - Increase `maintenance_work_mem` / `max_wal_size`  
  - Disable WAL Archiving During Load  
  - Run ANALYZE Afterwards  
- **5.5 Non-Durable Settings (for testing) (PostgreSQL Doc §14.5)**
- **5.6 Query Logging and Performance Measurement**

## 6. Beyond Indexing – Advanced Tuning Concepts
- **6.1 Query Rewriting and Optimization**
- **6.2 Partition Your Data (Tiger Data)**
- **6.3 Employ Partial Aggregation for Complex Queries (Tiger Data)**
- **6.4 Caching (Redis / Memcached)**
- **6.5 Connection Pooling (pgBouncer, HikariCP)**
- **6.6 Hardware and Memory Tuning**
- **6.7 Continuous Improvement & Upgrade Practice (Tiger Data)**

## 7. Case Study – Industry Example
- **7.1 E-commerce Checkout Delay**
- **7.2 Problem – 5 Table Join with `SELECT *`**
- **7.3 Actions – Index, Cache, Query Rewrite**
- **7.4 Result – 5 s → 0.7 s Response Time**

## 8. Lab Exercise
- **8.1 Create and Populate Orders Table**
- **8.2 Run Query and Measure Execution Time**
- **8.3 Add Index and Compare Performance**
- **8.4 Report Findings (Query Plan + Timing)**
- **8.5 Discussion of Performance Results**

## 9. Summary and Key Takeaways
- **9.1 Database Tuning is Continuous**
- **9.2 Indexing Gives Fastest Improvement**
- **9.3 Measure → Tune → Re-Measure**
- **9.4 Discussion: Real DB Issues in Student Projects**

## 10. References and Further Reading
- [PostgreSQL Documentation – Performance Tips](https://www.postgresql.org/docs/current/performance-tips.html)
- [Tiger Data – Best Practices for Query Optimization](https://www.tigerdata.com/blog/best-practices-for-query-optimization-in-postgresql)
- [PostgreSQL Wiki – Performance Optimization](https://wiki.postgresql.org/wiki/Performance_Optimization)
- [MySQL Performance Blog](https://www.percona.com/blog/)
- [Oracle AWR Reports Guide](https://docs.oracle.com/en/database/oracle/oracle-database/)
- [DB-Engines Benchmarks & Case Studies](https://db-engines.com/en/articles)

---

