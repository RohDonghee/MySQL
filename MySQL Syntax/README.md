# MySQL Study Notes

English study notes on core MySQL, organized by chapter and section. Technical details (syntax, data-type ranges, engine behavior) are cross-checked against the MySQL 8.0 Reference Manual.

## Sample database (`market_db`)

The examples assume a small shopping-mall database with two tables:

| Table | Meaning | Key columns |
| --- | --- | --- |
| `member` | Groups | `mem_id` (PK), `mem_name`, `mem_number`, `addr`, `phone1`, `phone2`, `height`, `debut_date` |
| `buy` | Purchases | `num` (PK, AUTO_INCREMENT), `mem_id` (FK → `member`), `prod_name`, `group_name`, `price`, `amount` |

## Index

| File | Topic |
| --- | --- |
| `ch1-1. Database Modeling.md` | Database modeling, project stages |
| `ch1-2. Database from Start to Finish.md` | Full DB lifecycle (create → insert → query) |
| `ch1-3. Database Objects.md` | Index / View / Stored Procedure (overview) |
| `ch2-1. SELECT-FROM-WHERE.md` | Core `SELECT … FROM … WHERE` |
| `ch2-2. Advanced SELECT.md` | `ORDER BY`, `LIMIT`, `DISTINCT`, `GROUP BY`, `HAVING` |
| `ch2-3. Data Manipulation (DML).md` | `INSERT` / `UPDATE` / `DELETE` |
| `ch3-1. MySQL Data Types.md` | Data types, variables, type conversion |
| `ch3-2. Joins.md` | Inner / outer / cross / self join |
| `ch3-3. SQL Programming.md` | `IF`, `CASE`, `WHILE`, dynamic SQL |
| `ch4-1. Creating Tables.md` | Designing & creating tables (GUI + SQL) |
| `ch4-2. Constraints.md` | PK / FK / UNIQUE / CHECK / DEFAULT |
| `ch4-3. Views.md` | Virtual tables (views) |
| `ch5-1. Index Concepts.md` | Clustered vs secondary index |
| `ch5-2. Index Internals.md` | B-tree structure & pages |
| `ch5-3. Using Indexes.md` | Create/drop indexes, when indexes fail |
| `ch6-1. Stored Procedures.md` | Stored procedures |
| `ch6-2. Stored Functions and Cursors.md` | Stored functions & cursors |
| `ch6-3. Triggers.md` | Triggers (NEW / OLD) |
| `ch7. Connecting SQL and Python.md` | Python environment, PyMySQL, tkinter GUI |
