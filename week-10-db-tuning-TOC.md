# Week 10 – Database Tuning
│
├── 1. Introduction
│   ├── 1.1 What is Database Performance?
│   ├── 1.2 What is Database Tuning?
│   ├── 1.3 Why Database Tuning is Needed
│
├── 2. Performance Problems in the Real World
│   ├── 2.1 Common Bottlenecks in Industry (EN-ID)
│   ├── 2.2 Case: Small vs Large Company Issues
│   ├── 2.3 Example: Slow Query in UMKM Database
│
├── 3. Core Concepts of Database Tuning
│   ├── 3.1 Overview of Tuning Areas
│   │    ├── Query Tuning
│   │    ├── Schema Tuning
│   │    ├── Index Tuning
│   │    ├── Memory / Configuration Tuning
│   │    └── Application-Level Tuning
│   ├── 3.2 How Tuning Improves Performance
│
├── 4. Indexing – The Heart of Tuning
│   ├── 4.1 What is an Index?
│   ├── 4.2 How Index Works (B-Tree, Hash)
│   ├── 4.3 SQL Example – CREATE INDEX
│   ├── 4.4 Comparing Query Time: With vs Without Index
│   ├── 4.5 Using EXPLAIN ANALYZE to Measure Query Plan
│
├── 5. Tools and Techniques for Performance Analysis
│   ├── 5.1 EXPLAIN / EXPLAIN ANALYZE
│   ├── 5.2 pg_stat_activity, Slow Query Log
│   ├── 5.3 VACUUM / ANALYZE in PostgreSQL
│   ├── 5.4 pgBadger, Percona Toolkit (optional)
│
├── 6. Beyond Indexing – Advanced Tuning Concepts
│   ├── 6.1 Query Rewriting
│   ├── 6.2 Partitioning
│   ├── 6.3 Caching (Redis / Memcached)
│   ├── 6.4 Connection Pooling
│   ├── 6.5 Hardware and Memory Tuning
│
├── 7. Case Study
│   ├── 7.1 E-commerce Checkout Delay
│   ├── 7.2 Problem – 5 Table Join with SELECT *
│   ├── 7.3 Actions – Index, Cache, Query Rewrite
│   ├── 7.4 Result – 5s → 0.7s Response Time
│
├── 8. Lab Exercise
│   ├── 8.1 Create and Populate Orders Table
│   ├── 8.2 Run Query and Measure Execution Time
│   ├── 8.3 Add Index and Compare Performance
│   ├── 8.4 Report Findings (execution plan + timing)
│
├── 9. Summary and Key Takeaways
│   ├── 9.1 Database Tuning is Continuous
│   ├── 9.2 Indexing Gives Fastest Improvement
│   ├── 9.3 Measure → Tune → Re-measure
│   └── 9.4 Discussion: Real DB issues in student projects
│
└── 10. References and Further Reading
     ├── PostgreSQL Documentation: Performance Tips
     ├── MySQL Performance Blog
     ├── Oracle AWR Reports Guide
     └── DB-Engines & Real Case Studies
