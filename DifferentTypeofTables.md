I think you mean **OLTP** and **OLAP**. Here's a real-world example showing how they differ.

| Feature    | OLTP (Online Transaction Processing) | OLAP (Online Analytical Processing)                          |
| ---------- | ------------------------------------ | ------------------------------------------------------------ |
| Purpose    | Run daily business operations        | Analyze historical data                                      |
| Data       | Current, detailed transactions       | Historical, aggregated data                                  |
| Users      | Cashiers, customers, employees       | Managers, analysts, executives                               |
| Operations | INSERT, UPDATE, DELETE               | SELECT, GROUP BY, SUM, AVG                                   |
| Database   | Normalized (3NF)                     | Star or Snowflake schema                                     |
| Example    | MySQL, MariaDB, PostgreSQL           | MariaDB (as a data warehouse), Snowflake, Redshift, BigQuery |

---

# Example 1: Supermarket

## OLTP Database

Every purchase is recorded immediately.

### Customer

| CustomerID | Name  |
| ---------- | ----- |
| C001       | Alice |
| C002       | Bob   |

### Product

| ProductID | ProductName | Price |
| --------- | ----------- | ----: |
| P001      | Laptop      |   900 |
| P002      | Mouse       |    25 |

### Sales

| SaleID | CustomerID | ProductID | Qty | SaleDate   |
| ------ | ---------- | --------- | --: | ---------- |
| 1001   | C001       | P001      |   1 | 2026-07-01 |
| 1002   | C002       | P002      |   2 | 2026-07-01 |

Every time someone buys something, a new row is inserted.

Typical OLTP query:

```sql
INSERT INTO Sales(CustomerID, ProductID, Qty, SaleDate)
VALUES ('C001', 'P002', 3, NOW());
```

Or:

```sql
UPDATE Product
SET Stock = Stock - 3
WHERE ProductID = 'P002';
```

These transactions must be fast and consistent.

---

# OLAP Data Warehouse

At the end of each day (or hour), the sales are loaded into the data warehouse.

## DimCustomer

| CustomerKey | CustomerName | City          |
| ----------: | ------------ | ------------- |
|           1 | Alice        | San Jose      |
|           2 | Bob          | San Francisco |

## DimProduct

| ProductKey | ProductName | Category    |
| ---------: | ----------- | ----------- |
|          1 | Laptop      | Electronics |
|          2 | Mouse       | Accessories |

## DimDate

|  DateKey | FullDate   | Month | Year |
| -------: | ---------- | ----- | ---- |
| 20260701 | 2026-07-01 | July  | 2026 |

## FactSales

|  DateKey | CustomerKey | ProductKey | Quantity | SalesAmount |
| -------: | ----------: | ---------: | -------: | ----------: |
| 20260701 |           1 |          1 |        1 |         900 |
| 20260701 |           2 |          2 |        2 |          50 |

Managers can now ask questions like:

* Which product category sold the most this year?
* Which city generated the highest revenue?
* What were monthly sales trends?
* Which customers spent the most?

Example OLAP query:

```sql
SELECT
    d.Year,
    p.Category,
    SUM(f.SalesAmount) AS TotalSales
FROM FactSales f
JOIN DimDate d
    ON f.DateKey = d.DateKey
JOIN DimProduct p
    ON f.ProductKey = p.ProductKey
GROUP BY d.Year, p.Category;
```

---

# Real Company Example (Amazon)

### OLTP

When you:

* Add an item to your cart
* Place an order
* Make a payment
* Update your shipping address

Amazon writes those changes immediately to its transactional databases.

Example:

```text
Order #12345
Customer: Alan
Product: iPhone
Quantity: 1
Status: Paid
```

---

### OLAP

Later, Amazon copies the transactional data into a data warehouse to answer questions like:

* Total revenue by month
* Best-selling products
* Sales by country
* Customer lifetime value
* Inventory trends
* Average delivery time

This analytical database is optimized for reading and reporting, not for processing individual customer transactions.

---

## Data Flow from OLTP to OLAP

```text
Customers
    │
    ▼
+----------------------+
| OLTP Database        |
| Orders               |
| Customers            |
| Products             |
| Payments             |
+----------------------+
          │
     ETL / ELT Process
          │
          ▼
+----------------------+
| OLAP Data Warehouse  |
| DimCustomer          |
| DimProduct           |
| DimDate              |
| FactSales            |
+----------------------+
          │
          ▼
Power BI / Tableau / Reports / Dashboards
```

If you're using **MariaDB as your data warehouse**, you'll typically have **one OLTP database** (the operational system) and **one separate MariaDB database** for the **OLAP/data warehouse**, where you organize the data into **dimension** and **fact** tables for reporting and analytics.
