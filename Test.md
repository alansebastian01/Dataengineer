Below is a complete MariaDB partitioning lab you can run in DBeaver.

MariaDB RANGE partitioning splits rows into contiguous, non-overlapping ranges, and `EXPLAIN PARTITIONS` helps verify partition pruning. ([MariaDB][1])

```sql
CREATE DATABASE IF NOT EXISTS partition_lab;
USE partition_lab;

DROP TABLE IF EXISTS sales_orders;

CREATE TABLE sales_orders (
    order_id BIGINT NOT NULL AUTO_INCREMENT,
    order_date DATE NOT NULL,
    customer_id INT NOT NULL,
    region VARCHAR(20) NOT NULL,
    amount DECIMAL(10,2) NOT NULL,
    status VARCHAR(20) NOT NULL,
    created_at DATETIME NOT NULL DEFAULT CURRENT_TIMESTAMP,

    PRIMARY KEY (order_id, order_date),
    KEY idx_order_date (order_date),
    KEY idx_customer_date (customer_id, order_date),
    KEY idx_status_date (status, order_date)
)
ENGINE = InnoDB
PARTITION BY RANGE COLUMNS(order_date) (
    PARTITION p2023q1 VALUES LESS THAN ('2023-04-01'),
    PARTITION p2023q2 VALUES LESS THAN ('2023-07-01'),
    PARTITION p2023q3 VALUES LESS THAN ('2023-10-01'),
    PARTITION p2023q4 VALUES LESS THAN ('2024-01-01'),
    PARTITION p2024q1 VALUES LESS THAN ('2024-04-01'),
    PARTITION p2024q2 VALUES LESS THAN ('2024-07-01'),
    PARTITION p2024q3 VALUES LESS THAN ('2024-10-01'),
    PARTITION p2024q4 VALUES LESS THAN ('2025-01-01'),
    PARTITION p_future VALUES LESS THAN (MAXVALUE)
);
```

Important rule: with partitioned tables, include the partition column in every unique key. That is why the primary key is `(order_id, order_date)`, not only `order_id`.

Load sample data:

```sql
SET max_recursive_iterations = 1000000;

INSERT INTO sales_orders
(order_date, customer_id, region, amount, status)
WITH RECURSIVE seq AS (
    SELECT 1 AS n
    UNION ALL
    SELECT n + 1 FROM seq WHERE n < 500000
)
SELECT
    DATE_ADD('2023-01-01', INTERVAL FLOOR(RAND() * 730) DAY),
    FLOOR(1 + RAND() * 50000),
    ELT(FLOOR(1 + RAND() * 4), 'WEST', 'EAST', 'NORTH', 'SOUTH'),
    ROUND(10 + RAND() * 990, 2),
    ELT(FLOOR(1 + RAND() * 4), 'NEW', 'PAID', 'SHIPPED', 'CANCELLED')
FROM seq;
```

Check partitions:

```sql
SELECT 
    PARTITION_NAME,
    TABLE_ROWS
FROM information_schema.PARTITIONS
WHERE TABLE_SCHEMA = 'partition_lab'
  AND TABLE_NAME = 'sales_orders';
```

Good query: should prune to only needed partitions.

```sql
EXPLAIN PARTITIONS
SELECT SUM(amount)
FROM sales_orders
WHERE order_date >= '2024-04-01'
  AND order_date <  '2024-07-01';
```

Bad query: may scan many/all partitions.

```sql
EXPLAIN PARTITIONS
SELECT SUM(amount)
FROM sales_orders
WHERE YEAR(order_date) = 2024;
```

Better version:

```sql
EXPLAIN PARTITIONS
SELECT SUM(amount)
FROM sales_orders
WHERE order_date >= '2024-01-01'
  AND order_date <  '2025-01-01';
```

Useful analytics:

```sql
SELECT 
    DATE_FORMAT(order_date, '%Y-%m') AS order_month,
    COUNT(*) AS orders,
    ROUND(SUM(amount), 2) AS revenue
FROM sales_orders
WHERE order_date >= '2024-01-01'
  AND order_date <  '2025-01-01'
GROUP BY DATE_FORMAT(order_date, '%Y-%m')
ORDER BY order_month;
```

Drop old data fast:

```sql
ALTER TABLE sales_orders DROP PARTITION p2023q1;
```

Add future partition:

```sql
ALTER TABLE sales_orders
REORGANIZE PARTITION p_future INTO (
    PARTITION p2025q1 VALUES LESS THAN ('2025-04-01'),
    PARTITION p_future VALUES LESS THAN (MAXVALUE)
);
```

Partitioning is best when queries often filter by the partition column, such as `order_date`.

[1]: https://mariadb.com/docs/server/server-usage/partitioning-tables/partitioning-types/range-partitioning-type?utm_source=chatgpt.com "RANGE Partitioning Type | Server | MariaDB Documentation"
