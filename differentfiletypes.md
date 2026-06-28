
In data engineering and data warehousing, you'll encounter several different file types. Here's a quick reference you can use for interviews or exams.

| File Type    | Extension       | Human Readable | Structure              | Common Use                    |
| ------------ | --------------- | -------------- | ---------------------- | ----------------------------- |
| **CSV**      | `.csv`          | ✅ Yes          | Tabular                | Data exchange, Excel exports  |
| **JSON**     | `.json`         | ✅ Yes          | Nested/Semi-structured | APIs, web applications        |
| **XML**      | `.xml`          | ✅ Yes          | Hierarchical           | Enterprise systems, SOAP APIs |
| **YAML**     | `.yaml`, `.yml` | ✅ Yes          | Key-value              | Configuration files           |
| **Excel**    | `.xlsx`, `.xls` | ✅ Yes          | Spreadsheet            | Business reports              |
| **TXT**      | `.txt`          | ✅ Yes          | Plain text             | Logs, simple data             |
| **TSV**      | `.tsv`          | ✅ Yes          | Tab-separated          | Similar to CSV                |
| **Parquet**  | `.parquet`      | ❌ No           | Columnar Binary        | Data warehouses, Spark        |
| **ORC**      | `.orc`          | ❌ No           | Columnar Binary        | Hive, Hadoop                  |
| **Avro**     | `.avro`         | ❌ No           | Row-based Binary       | Kafka, streaming              |
| **SQL Dump** | `.sql`          | ✅ Yes          | SQL statements         | Database backup/migration     |
| **Log File** | `.log`          | ✅ Yes          | Text                   | Application and server logs   |

---

## 1. CSV (Comma-Separated Values)

```csv
id,title,platform
1,Elden Ring,PS5
2,Minecraft,PC
```

**Used for:**

* Data import/export
* Excel
* Simple datasets

---

## 2. JSON (JavaScript Object Notation)

```json
{
  "id": 1,
  "title": "Elden Ring",
  "platform": "PS5"
}
```

**Used for:**

* REST APIs
* NoSQL databases
* Web applications

---

## 3. XML (eXtensible Markup Language)

```xml
<game>
  <id>1</id>
  <title>Elden Ring</title>
  <platform>PS5</platform>
</game>
```

**Used for:**

* Banking
* Government systems
* SOAP web services

---

## 4. YAML

```yaml
id: 1
title: Elden Ring
platform: PS5
```

**Used for:**

* Docker Compose
* Kubernetes
* GitHub Actions
* Configuration files

---

## 5. Excel

| id | title      | platform |
| -- | ---------- | -------- |
| 1  | Elden Ring | PS5      |

**Used for:**

* Business reports
* Manual data entry
* Financial spreadsheets

---

## 6. TXT

```text
Elden Ring
PlayStation 5
145 Hours
```

**Used for:**

* Simple text data
* Logs
* Notes

---

## 7. TSV (Tab-Separated Values)

```text
id	title	platform
1	Elden Ring	PS5
2	Minecraft	PC
```

**Used for:**

* Similar to CSV but uses tabs instead of commas

---

## 8. Parquet

* Binary format
* Columnar storage
* Compressed
* Fast analytics

**Used for:**

* Spark
* Snowflake
* Databricks
* BigQuery

---

## 9. ORC

* Binary format
* Columnar storage
* Optimized for Hive

**Used for:**

* Hadoop
* Hive
* Spark

---

## 10. Avro

* Binary format
* Row-based
* Includes schema

**Used for:**

* Kafka
* Streaming
* ETL pipelines

---

## 11. SQL Dump

```sql
CREATE TABLE Games (
    id INT,
    title VARCHAR(100)
);

INSERT INTO Games VALUES (1,'Elden Ring');
```

**Used for:**

* Database backup
* Database migration

---

## 12. Log File

```text
2026-06-28 09:00:01 User Login
2026-06-28 09:00:10 Game Started
```

**Used for:**

* Monitoring
* Troubleshooting
* Auditing

---

# Interview Summary

| Question               | Best Answer |
| ---------------------- | ----------- |
| Best for APIs          | JSON        |
| Best for configuration | YAML        |
| Best for spreadsheets  | CSV / Excel |
| Best for analytics     | Parquet     |
| Best for Hadoop        | ORC         |
| Best for Kafka         | Avro        |
| Best for backups       | SQL Dump    |
| Best for logs          | TXT / LOG   |

## Memory Trick

* **CSV** → Spreadsheet data
* **JSON** → APIs
* **XML** → Enterprise systems
* **YAML** → Configuration
* **Parquet** → Analytics
* **ORC** → Hive/Hadoop
* **Avro** → Streaming/Kafka
* **SQL** → Database backup
* **LOG/TXT** → Application logs

These are the file formats most commonly discussed in data engineering, ETL, Azure Data Factory, Snowflake, Databricks, and data warehouse interviews.
