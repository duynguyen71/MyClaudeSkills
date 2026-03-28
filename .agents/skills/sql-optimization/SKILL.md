---
name: sql-optimization
description: 'Universal SQL performance optimization assistant for comprehensive query tuning, indexing strategies, and database performance analysis across all SQL databases (MySQL, PostgreSQL, SQL Server, Oracle). Provides execution plan analysis, pagination optimization, batch operations, and performance monitoring guidance.'
---

# SQL Performance Optimization Assistant

Expert SQL performance optimization for ${selection} (or entire project if no selection). Focus on universal SQL optimization techniques that work across MySQL, PostgreSQL, SQL Server, Oracle, and other SQL databases.

## 🎯 Core Optimization Areas

### Query Performance Analysis
```sql
-- ❌ BAD: Inefficient query patterns
SELECT * FROM "orders" 'o'
WHERE YEAR("o"."created_at") = 2024
  AND "o"."customer_id" IN (
      SELECT "c"."id" FROM "customers" 'c' WHERE "c"."status" = 'active'
  );

-- ✅ GOOD: Optimized query with proper indexing hints
SELECT "o"."id", "o"."customer_id", "o"."total_amount", "o"."created_at"
FROM "orders" 'o'
INNER JOIN "customers" 'c' ON "o"."customer_id" = "c"."id"
WHERE "o"."created_at" >= '2024-01-01'
  AND "o"."created_at" < '2025-01-01'
  AND "c"."status" = 'active';

-- Required indexes:
-- CREATE INDEX "idx_orders_created_at" ON "orders"("created_at");
-- CREATE INDEX "idx_customers_status" ON "customers"("status");
-- CREATE INDEX "idx_orders_customer_id" ON "orders"("customer_id");
```

### Index Strategy Optimization
```sql
-- ❌ BAD: Poor indexing strategy
CREATE INDEX "idx_user_data" ON "users"("email", "first_name", "last_name", "created_at");

-- ✅ GOOD: Optimized composite indexing
-- For queries filtering by email first, then sorting by created_at
CREATE INDEX "idx_users_email_created" ON "users"("email", "created_at");

-- For full-text name searches
CREATE INDEX "idx_users_name" ON "users"("last_name", "first_name");

-- For user status queries
CREATE INDEX "idx_users_status_created" ON "users"("status", "created_at")
WHERE "status" IS NOT NULL;
```

### Subquery Optimization
```sql
-- ❌ BAD: Correlated subquery
SELECT "p"."product_name", "p"."price"
FROM "products" 'p'
WHERE "p"."price" > (
    SELECT AVG("price")
    FROM "products" 'p2'
    WHERE "p2"."category_id" = "p"."category_id"
);

-- ✅ GOOD: Window function approach
SELECT "product_name", "price"
FROM (
    SELECT "product_name", "price",
           AVG("price") OVER (PARTITION BY "category_id") as 'avg_category_price'
    FROM "products"
) 'ranked'
WHERE "price" > "avg_category_price";
```

## 📊 Performance Tuning Techniques

### JOIN Optimization
```sql
-- ❌ BAD: Inefficient JOIN order and conditions
SELECT "o".*, "c"."name", "p"."product_name"
FROM "orders" 'o'
LEFT JOIN "customers" 'c' ON "o"."customer_id" = "c"."id"
LEFT JOIN "order_items" 'oi' ON "o"."id" = "oi"."order_id"
LEFT JOIN "products" 'p' ON "oi"."product_id" = "p"."id"
WHERE "o"."created_at" > '2024-01-01'
  AND "c"."status" = 'active';

-- ✅ GOOD: Optimized JOIN with filtering
SELECT "o"."id", "o"."total_amount", "c"."name", "p"."product_name"
FROM "orders" 'o'
INNER JOIN "customers" 'c' ON "o"."customer_id" = "c"."id" AND "c"."status" = 'active'
INNER JOIN "order_items" 'oi' ON "o"."id" = "oi"."order_id"
INNER JOIN "products" 'p' ON "oi"."product_id" = "p"."id"
WHERE "o"."created_at" > '2024-01-01';
```

### Pagination Optimization
```sql
-- ❌ BAD: OFFSET-based pagination (slow for large offsets)
SELECT * FROM "products"
ORDER BY "created_at" DESC
LIMIT 20 OFFSET 10000;

-- ✅ GOOD: Cursor-based pagination
SELECT * FROM "products"
WHERE "created_at" < '2024-06-15 10:30:00'
ORDER BY "created_at" DESC
LIMIT 20;

-- Or using ID-based cursor
SELECT * FROM "products"
WHERE "id" > 1000
ORDER BY "id"
LIMIT 20;
```

### Aggregation Optimization
```sql
-- ❌ BAD: Multiple separate aggregation queries
SELECT COUNT(*) FROM "orders" WHERE "status" = 'pending';
SELECT COUNT(*) FROM "orders" WHERE "status" = 'shipped';
SELECT COUNT(*) FROM "orders" WHERE "status" = 'delivered';

-- ✅ GOOD: Single query with conditional aggregation
SELECT
    COUNT(CASE WHEN "status" = 'pending' THEN 1 END) as 'pending_count',
    COUNT(CASE WHEN "status" = 'shipped' THEN 1 END) as 'shipped_count',
    COUNT(CASE WHEN "status" = 'delivered' THEN 1 END) as 'delivered_count'
FROM "orders";

-- COUNT variations and their use cases:
-- COUNT(*) - Counts all rows including NULLs (fastest for total row count)
-- COUNT(1) - Equivalent to COUNT(*) in modern databases (no performance difference)
-- COUNT("field") - Counts only non-NULL values in the specified field
SELECT
    COUNT(*) as 'total_rows',           -- All rows
    COUNT(1) as 'total_rows_alt',       -- Same as COUNT(*)
    COUNT("email") as 'rows_with_email' -- Only rows where email IS NOT NULL
FROM "customers";
```

## 🔍 Query Anti-Patterns

### SELECT Performance Issues
```sql
-- ❌ BAD: SELECT * anti-pattern
SELECT * FROM "large_table" 'lt'
JOIN "another_table" 'at' ON "lt"."id" = "at"."ref_id";

-- ✅ GOOD: Explicit column selection
SELECT "lt"."id", "lt"."name", "at"."value"
FROM "large_table" 'lt'
JOIN "another_table" 'at' ON "lt"."id" = "at"."ref_id";
```

### WHERE Clause Optimization
```sql
-- ❌ BAD: Function calls in WHERE clause
SELECT * FROM "orders"
WHERE UPPER("customer_email") = 'JOHN@EXAMPLE.COM';

-- ✅ GOOD: Index-friendly WHERE clause
SELECT * FROM "orders"
WHERE "customer_email" = 'john@example.com';
-- Consider: CREATE INDEX "idx_orders_email" ON "orders"(LOWER("customer_email"));

-- ❌ BAD: String comparison with timestamp field
SELECT * FROM "orders"
WHERE "created_at" > '2024-01-01 00:00:00';

-- ✅ GOOD: Proper timestamp parsing for comparison
SELECT * FROM "orders"
WHERE "created_at" > TIMESTAMP '2024-01-01 00:00:00';
-- Or database-specific functions:
-- PostgreSQL: WHERE "created_at" > '2024-01-01 00:00:00'::TIMESTAMP
-- MySQL: WHERE "created_at" > STR_TO_DATE('2024-01-01 00:00:00', '%Y-%m-%d %H:%i:%s')
-- SQL Server: WHERE "created_at" > CAST('2024-01-01 00:00:00' AS DATETIME)

-- ❌ BAD: Using TRUNC in WHERE clause (prevents index usage)
SELECT * FROM "orders"
WHERE TRUNC("created_at") = DATE '2024-01-01';

-- ✅ GOOD: Date range comparison for date-only matching
SELECT * FROM "orders"
WHERE "created_at" >= DATE '2024-01-01'
  AND "created_at" < DATE '2024-01-02';
-- This approach allows index usage on created_at

-- ✅ ACCEPTABLE: TRUNC in SELECT for display purposes only
SELECT TRUNC("created_at") as 'order_date', COUNT(*) as 'order_count'
FROM "orders"
WHERE "created_at" >= DATE '2024-01-01'
  AND "created_at" < DATE '2024-02-01'
GROUP BY TRUNC("created_at");

-- ⚠️ IMPORTANT: Check server and database timezone before date/time comparisons
-- Oracle:
SELECT DBTIMEZONE as 'db_timezone', SESSIONTIMEZONE as 'session_timezone' FROM DUAL;

-- PostgreSQL:
SELECT current_setting('TIMEZONE') as 'db_timezone';
SHOW TIMEZONE;

-- MySQL:
SELECT @@global.time_zone as 'global_tz', @@session.time_zone as 'session_tz';

-- SQL Server:
SELECT SYSDATETIMEOFFSET() as 'server_time_with_offset';
SELECT CURRENT_TIMEZONE() as 'current_timezone'; -- SQL Server 2022+

-- ✅ GOOD: Timezone-aware comparisons
-- Convert to UTC or specific timezone before comparison
SELECT * FROM "orders"
WHERE "created_at" AT TIME ZONE 'UTC' >= TIMESTAMP '2024-01-01 00:00:00';
```

### OR vs UNION Optimization
```sql
-- ❌ BAD: Complex OR conditions
SELECT * FROM "products"
WHERE ("category" = 'electronics' AND "price" < 1000)
   OR ("category" = 'books' AND "price" < 50);

-- ✅ GOOD: UNION approach for better optimization
SELECT * FROM "products" WHERE "category" = 'electronics' AND "price" < 1000
UNION ALL
SELECT * FROM "products" WHERE "category" = 'books' AND "price" < 50;
```

## 📈 Database-Agnostic Optimization

### Batch Operations
```sql
-- ❌ BAD: Row-by-row operations
INSERT INTO "products" ("name", "price") VALUES ('Product 1', 10.00);
INSERT INTO "products" ("name", "price") VALUES ('Product 2', 15.00);
INSERT INTO "products" ("name", "price") VALUES ('Product 3', 20.00);

-- ✅ GOOD: Batch insert
INSERT INTO "products" ("name", "price") VALUES
('Product 1', 10.00),
('Product 2', 15.00),
('Product 3', 20.00);
```

### Temporary Table Usage
```sql
-- ✅ GOOD: Using temporary tables for complex operations
CREATE TEMPORARY TABLE "temp_calculations" AS
SELECT "customer_id",
       SUM("total_amount") as 'total_spent',
       COUNT(*) as 'order_count'
FROM "orders"
WHERE "created_at" >= '2024-01-01'
GROUP BY "customer_id";

-- Use the temp table for further calculations
SELECT "c"."name", "tc"."total_spent", "tc"."order_count"
FROM "temp_calculations" 'tc'
JOIN "customers" 'c' ON "tc"."customer_id" = "c"."id"
WHERE "tc"."total_spent" > 1000;
```

## 🛠️ Index Management

### Index Design Principles
```sql
-- ✅ GOOD: Covering index design
CREATE INDEX "idx_orders_covering"
ON "orders"("customer_id", "created_at")
INCLUDE ("total_amount", "status");  -- SQL Server syntax
-- Or: CREATE INDEX "idx_orders_covering" ON "orders"("customer_id", "created_at", "total_amount", "status"); -- Other databases
```

### Partial Index Strategy
```sql
-- ✅ GOOD: Partial indexes for specific conditions
CREATE INDEX "idx_orders_active"
ON "orders"("created_at")
WHERE "status" IN ('pending', 'processing');
```

### Parallel Query Hints in Views
```sql
-- ✅ GOOD: Parallelizing large table scans in views
-- Use when the view wraps a table or join so large that serial scans become a bottleneck
CREATE OR REPLACE VIEW "v_sales_filtered" AS
SELECT /*+ PARALLEL(16) */
       "DATE_KEY",
       "STORE_ID",
       "PRODUCT_ID",
       "AMOUNT",
       "QUANTITY"
FROM "FACT_SALES"
WHERE "DATE_KEY" >= DATE '2025-01-01';

-- Queries using this view automatically benefit from parallel execution
SELECT "STORE_ID", SUM("AMOUNT") as 'total_amount'
FROM "v_sales_filtered"
GROUP BY "STORE_ID";

-- Common use cases:
-- - Data warehouse ETL views
-- - Materialization staging views
-- - Pre-filtered fact table views
-- - Heavy reporting views with full scans of huge tables (billions of rows)
```

## 📊 Performance Monitoring Queries

### Query Performance Analysis
```sql
-- Generic approach to identify slow queries
-- (Specific syntax varies by database)

-- For MySQL:
SELECT "query_time", "lock_time", "rows_sent", "rows_examined", "sql_text"
FROM "mysql"."slow_log"
ORDER BY "query_time" DESC;

-- For PostgreSQL:
SELECT "query", "calls", "total_time", "mean_time"
FROM "pg_stat_statements"
ORDER BY "total_time" DESC;

-- For SQL Server:
SELECT
    "qs"."total_elapsed_time"/"qs"."execution_count" as 'avg_elapsed_time',
    "qs"."execution_count",
    SUBSTRING("qt"."text", ("qs"."statement_start_offset"/2)+1,
        ((CASE "qs"."statement_end_offset" WHEN -1 THEN DATALENGTH("qt"."text")
        ELSE "qs"."statement_end_offset" END - "qs"."statement_start_offset")/2)+1) as 'query_text'
FROM "sys"."dm_exec_query_stats" 'qs'
CROSS APPLY sys.dm_exec_sql_text("qs"."sql_handle") 'qt'
ORDER BY "avg_elapsed_time" DESC;
```

## 🎯 Universal Optimization Checklist

### Query Structure
- [ ] Avoiding SELECT * in production queries
- [ ] Using appropriate JOIN types (INNER vs LEFT/RIGHT)
- [ ] Filtering early in WHERE clauses
- [ ] Using EXISTS instead of IN for subqueries when appropriate
- [ ] Avoiding functions in WHERE clauses that prevent index usage

### Index Strategy
- [ ] Creating indexes on frequently queried columns
- [ ] Using composite indexes in the right column order
- [ ] Avoiding over-indexing (impacts INSERT/UPDATE performance)
- [ ] Using covering indexes where beneficial
- [ ] Creating partial indexes for specific query patterns

### Data Types and Schema
- [ ] Using appropriate data types for storage efficiency
- [ ] Normalizing appropriately (3NF for OLTP, denormalized for OLAP)
- [ ] Using constraints to help query optimizer
- [ ] Partitioning large tables when appropriate

### Query Patterns
- [ ] Using LIMIT/TOP for result set control
- [ ] Implementing efficient pagination strategies
- [ ] Using batch operations for bulk data changes
- [ ] Avoiding N+1 query problems
- [ ] Using prepared statements for repeated queries

### Performance Testing
- [ ] Testing queries with realistic data volumes
- [ ] Analyzing query execution plans
- [ ] Monitoring query performance over time
- [ ] Setting up alerts for slow queries
- [ ] Regular index usage analysis

## 📝 Optimization Methodology

1. **Identify**: Use database-specific tools to find slow queries
2. **Analyze**: Examine execution plans and identify bottlenecks
3. **Optimize**: Apply appropriate optimization techniques
4. **Test**: Verify performance improvements
5. **Monitor**: Continuously track performance metrics
6. **Iterate**: Regular performance review and optimization

Focus on measurable performance improvements and always test optimizations with realistic data volumes and query patterns.
