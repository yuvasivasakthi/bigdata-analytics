# 🐘 Big Data Analytics — Lab Exercises

A collection of hands-on Big Data Analytics experiments implemented using **Apache Hadoop**, **Apache Pig**, and **Apache Hive** as part of coursework. Covers the complete big data stack from HDFS setup to distributed processing and data warehousing.

---

## 🛠️ Technologies Used

| Tool | Purpose |
|------|---------|
| Apache Hadoop (HDFS) | Distributed file storage |
| MapReduce (Java) | Parallel data processing |
| Apache Pig | High-level data flow scripting |
| Apache Hive | SQL-like data warehousing |

---

## 📁 Exercises Overview

### Ex 1 — Hadoop Installation & HDFS Setup
- Installed Apache Hadoop in pseudo-distributed mode
- Configured `core-site.xml`, `hdfs-site.xml`, `mapred-site.xml`, and `yarn-site.xml`
- Formatted the NameNode and started HDFS + YARN daemons
- Verified cluster health using `jps` and the Hadoop Web UI

### Ex 3 — File Transfer to HDFS
- Transferred local files to HDFS using `hadoop fs -put`
- Listed, viewed, and managed files on the Hadoop Distributed File System
- Practiced basic HDFS shell commands (`ls`, `mkdir`, `cat`, `rm`)

### Ex 4 — MapReduce Basics
- Understood the MapReduce programming model (Input → Split → Map → Shuffle → Reduce → Output)
- Ran built-in MapReduce examples on HDFS data

### Ex 5 — Word Count (MapReduce in Java)
- Implemented the classic **Word Count** program using the Hadoop MapReduce API in Java
- **Mapper**: Tokenizes each input line and emits `(word, 1)` pairs
- **Reducer**: Aggregates counts per word using summation
- Compiled and executed the JAR on HDFS input files
- **Key Concepts**: `Mapper`, `Reducer`, `IntWritable`, `Text`, `Job` configuration

### Ex 6 — Stop Word Removal (MapReduce in Java)
- Extended Word Count to **filter stop words** (e.g., "is", "the", "and") from frequency output
- Used **Hadoop Distributed Cache** to load a stop-word list file across all nodes
- Implemented `setup()` method in the Mapper to load patterns from HDFS cache at runtime
- Applied `regex`-based word boundary splitting for accurate tokenization
- **Key Concepts**: `DistributedCache`, `URI`, `HashSet`, `Pattern`, `BufferedReader`

### Ex 7 — Weather Data Analysis (MapReduce in Java)
- Analyzed large weather datasets to identify **Hot Days** (temp > 35°C) and **Cold Days** (temp < 10°C)
- Mapper parses fixed-width text records extracting date, max temperature, and min temperature
- Reducer outputs the classified days with their temperature values
- **Key Concepts**: Fixed-width parsing, `Float.parseFloat()`, conditional emit logic

### Ex 8 — Purchase Dataset Analysis
- Loaded a purchase transaction dataset into HDFS
- Analyzed fields like customer ID, product, quantity, and price for aggregation exercises

### Ex 9 — Apache Pig Installation
- Installed Apache Pig and configured it to run in **MapReduce mode** over Hadoop
- Verified installation with `pig -version` and ran basic Pig Latin scripts

### Ex 10 — Apache Pig — Data Operations
Performed multiple relational operations on student and customer datasets using **Pig Latin**:
- `LOAD` — Load structured CSV data from HDFS using `PigStorage`
- `ORDER BY` — Sort student records by age in descending order
- `GROUP BY` — Group students by age for aggregation
- `JOIN` — Inner join between `customers` and `orders` tables
- `LEFT/RIGHT/FULL OUTER JOIN` — Relational outer joins
- `FILTER` — Filter students by city (e.g., Chennai)
- `FOREACH GENERATE` — Project specific columns (id, age, city)

### Ex 11 — TF-IDF Computation using Apache Pig
- Computed **TF-IDF (Term Frequency–Inverse Document Frequency)** scores for a book dataset
- Multi-job Pig Latin pipeline:
  - **Job 1**: Tokenize text and group by (word, file) → count term frequency `n`
  - **Job 2**: Compute total words per file `N` (normalization)
  - **Job 3**: Count documents containing each word `m` (for IDF)
  - **Job 4**: Calculate final TF-IDF = `(n/N) * log(10/m)`
- Stored output to HDFS using `store ... into`
- **Key Concepts**: TF-IDF, `TOKENIZE`, `FLATTEN`, multi-pass aggregation

### Ex 12 — Apache Hive Installation
- Installed Apache Hive and configured the Hive Metastore
- Connected Hive to the Hadoop cluster for SQL-based analytics

### Ex 13 — Apache Hive Queries
- Created Hive tables and loaded data from HDFS
- Ran HiveQL queries: `SELECT`, `WHERE`, `GROUP BY`, `ORDER BY`, `JOIN`
- Used Hive for structured data warehousing on top of HDFS

---

## 🚀 How to Run (Example: Word Count)

```bash
# Compile
javac -classpath $(hadoop classpath) -d wordcount_classes WordCount.java
jar -cvf wordcount.jar -C wordcount_classes/ .

# Upload input to HDFS
hadoop fs -mkdir /input
hadoop fs -put input.txt /input/

# Run
hadoop jar wordcount.jar WordCount /input /output

# View results
hadoop fs -cat /output/part-r-00000
```

---

## 📚 Key Concepts Learned

- HDFS architecture: NameNode, DataNode, blocks, replication
- MapReduce paradigm: partitioning, shuffling, sorting, combining
- Distributed cache for sharing files across cluster nodes
- Apache Pig Latin for ETL and data transformation pipelines
- TF-IDF algorithm for text relevance scoring
- Apache Hive for SQL analytics on big data

---

## 🏷️ Tags

`Hadoop` `MapReduce` `HDFS` `Apache Pig` `Apache Hive` `Big Data` `Java` `TF-IDF` `Data Analytics`
