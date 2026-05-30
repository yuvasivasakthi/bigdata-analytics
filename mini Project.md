# 🛒 Mini Project: Customer Order Analytics using Apache Hive & Pig

## 📌 Problem Statement

Analysis of **customer order data** using Apache Hive and Apache Pig on a Hadoop cluster.
The dataset contains order records with fields: `ordernumber`, `status`, `city`, and `customerName`.

The project demonstrates how to:
- Store and query structured data using **Apache Hive (HiveQL)**
- Process and transform data at scale using **Apache Pig (Pig Latin)**

---

## 📂 Dataset

| Field | Type | Description |
|-------|------|-------------|
| ordernumber | INT | Unique order ID |
| status | STRING | Order status (Shipped / Disputed) |
| city | STRING | Customer city |
| customerName | STRING | Name of the customer |

**Sample Records:**

| ordernumber | status | city | customerName |
|-------------|--------|------|--------------|
| 01 | Shipped | Paris | Emma |
| 02 | Shipped | San Francisco | Harry |
| 03 | Disputed | Singapore | Yuki |
| 04 | Shipped | Paris | Chris |
| 05 | Disputed | San Francisco | Luisa |

---

## 🐝 Apache Hive — Operations

Apache Hive enables SQL-like querying on top of Hadoop HDFS, suitable for managing petabytes of data.

### 1. Create Table
```sql
CREATE TABLE dataset (
  ordernumber INT,
  status STRING,
  city STRING,
  customerName STRING
);
```

### 2. Insert Records
```sql
INSERT INTO dataset VALUES (01, 'Shipped', 'Paris', 'Emma');
INSERT INTO dataset VALUES (02, 'Shipped', 'San Francisco', 'Harry');
INSERT INTO dataset VALUES (03, 'Disputed', 'Singapore', 'Yuki');
INSERT INTO dataset VALUES (04, 'Shipped', 'Paris', 'Chris');
INSERT INTO dataset VALUES (05, 'Disputed', 'San Francisco', 'Luisa');
```

### 3. Select All Records
```sql
SELECT * FROM dataset;
```

### 4. Select Specific Columns
```sql
SELECT customerName, status FROM dataset;
```

### 5. Count Total Records
```sql
SELECT COUNT(*) FROM dataset;
```

### 6. Order Records by Status
```sql
SELECT ordernumber, customerName, status
FROM dataset
ORDER BY status;
```

### 7. Group Orders by City
```sql
SELECT city, COUNT(*)
FROM dataset
GROUP BY city;
```
> Shows how many orders came from each city.

### 8. Rename Table (ALTER TABLE)
```sql
ALTER TABLE dataset RENAME TO orderdet;
```

---

## 🐷 Apache Pig — Operations

Apache Pig provides a high-level scripting language (Pig Latin) that compiles down to MapReduce jobs, making it easier to process large datasets without writing Java code.

### 1. Start Pig in Local Mode
```pig
pig -x local
```

### 2. Load Dataset from HDFS
```pig
dataset = LOAD '/home/hadoop/dataset.txt'
  USING PigStorage(',')
  AS (ordernumber:int, status:chararray, city:chararray, customerName:chararray);

DUMP dataset;
```

### 3. Group Orders by Status
```pig
data = GROUP dataset BY status;
DUMP data;
```
> Groups all orders into "Shipped" and "Disputed" buckets.

### 4. Order Dataset by City (Ascending)
```pig
city_order = ORDER dataset BY city ASC;
DUMP city_order;
```

### 5. Join Two Datasets
```pig
dataset1 = LOAD '/home/hadoop/dataset1.txt'
  USING PigStorage(',')
  AS (ordernumber:int, status:chararray, city:chararray, customerName:chararray);

dataset3 = JOIN dataset BY ordernumber, dataset1 BY ordernumber;
DUMP dataset3;
```
> Inner join on `ordernumber` — combines records from both files.

### 6. Limit Output Records
```pig
city_limit = LIMIT dataset 2;
DUMP city_limit;
```
> Returns only the first 2 records.

---

## 🧠 Key Concepts Covered

- **HiveQL**: DDL (`CREATE`, `ALTER`) and DML (`INSERT`, `SELECT`, `GROUP BY`, `ORDER BY`, `COUNT`)
- **Pig Latin**: `LOAD`, `DUMP`, `GROUP BY`, `ORDER BY`, `JOIN`, `LIMIT`
- **HDFS**: Data storage and retrieval using `PigStorage`
- **Hive Metastore**: Table schema management on top of Hadoop
- **MapReduce Abstraction**: Pig Latin compiles each operation into MapReduce jobs automatically

---

## 🔧 Tools & Technologies

`Apache Hadoop` · `Apache Hive` · `Apache Pig` · `HiveQL` · `Pig Latin` · `HDFS`

---

## 📊 Operations Summary

| Operation | Hive | Pig |
|-----------|------|-----|
| Load Data | `INSERT INTO` | `LOAD ... USING PigStorage` |
| View Data | `SELECT *` | `DUMP` |
| Filter | `WHERE` | `FILTER BY` |
| Count | `COUNT(*)` | `COUNT()` in GROUP |
| Group | `GROUP BY` | `GROUP BY` |
| Sort | `ORDER BY` | `ORDER BY ASC/DESC` |
| Join | `JOIN` | `JOIN ... BY` |
| Limit | `LIMIT n` | `LIMIT n` |
| Rename Table | `ALTER TABLE RENAME` | — |
