# 🧭 Big Data Ecosystem Overview

This document explains how the main components of the Hadoop-based Big Data ecosystem connect and work together: **Hue, Hive, Impala, HDFS, Spark (PySpark), HBase, Iceberg, Parquet, ORC, Oozie**, and **Teradata**.

---

## 🧱 Core Components and Their Roles

| Component       | Type                     | Purpose                                                                 |
|------------------|--------------------------|-------------------------------------------------------------------------|
| **HDFS**         | Storage                  | Distributed file system for storing large datasets across cluster nodes. |
| **Hive**         | SQL Engine               | Batch SQL engine for data warehousing and ETL.                          |
| **Impala**       | SQL Engine               | Low‐latency, interactive SQL engine for analytics.                       |
| **Hue**          | Web UI                   | Web-based interface to interact with Hadoop ecosystem tools.            |
| **Spark / PySpark** | Processing Engine     | Distributed computing engine for data processing, ETL, ML, analytics.   |
| **Iceberg**      | Table Format             | Modern table layer adding ACID transactions, schema evolution, time travel. |
| **HBase**        | NoSQL Database           | Real-time read/write access to data stored on HDFS.                      |
| **Parquet / ORC**| File Formats             | Columnar storage formats optimized for big data analytics.               |
| **Oozie**        | Workflow Scheduler       | Orchestrates and schedules Hadoop ecosystem jobs (Hive, Spark, etc.).    |
| **Teradata**     | Enterprise Data Warehouse| MPP SQL data warehouse for large-scale structured analytics.             |

---

## 🔗 Ecosystem Architecture Flow

```text
                ┌────────────────────┐
                │        Hue         │
                │ (Web UI for Hadoop)│
                │ - Run Hive/Impala  │
                │ - Browse HDFS/HBase│
                └─────────┬──────────┘
                          │
          ┌───────────────┼───────────────────┐
          │                                   │
  ┌───────▼─────────┐                 ┌───────▼─────────┐
  │      Hive        │                │     Impala       │
  │ (Batch SQL Engine)│               │ (Fast SQL Engine)│
  │ - ETL / Warehousing│              │ - Interactive BI │
  │ - Works with Oozie │              │                  │
  └────────┬─────────┘                 └────────┬─────────┘
           │                                     │
           │ (Both use the same Hive Metastore)  │
           └────────────────┬────────────────────┘
                            │
                     ┌──────▼───────┐
                     │   Iceberg    │
                     │ Modern Table │
                     │   Format     │
                     │ (ACID, schema│
                     │ evolution)   │
                     └──────┬───────┘
                            │
                    ┌───────▼────────┐
                    │     HDFS       │
                    │ (Data Storage) │
                    └───────┬────────┘
                            │
        ┌───────────────────┼────────────────────────────┐
        │                                           │
 ┌──────▼───────┐                             ┌────────▼─────────┐
 │   PySpark     │                             │     HBase        │
 │ (Compute / ETL)│                            │ (NoSQL, Real-time)│
 │ - Reads/Writes │                            │ - Random R/W      │
 │   to HDFS/Iceberg/Hive                     │ - Built on HDFS   │
 └───────────────┘                             └────────┬─────────┘
                                                       │
                                       ┌───────────────▼─────────────┐
                                       │        Teradata             │
                                       │ Enterprise Data Warehouse   │
                                       │ (Structured large-scale SQL)│
                                       └─────────────────────────────┘

````

---

## 📂 Data Storage Layer — HDFS

**HDFS (Hadoop Distributed File System)** is the foundation where all raw and processed data is stored.

* Stores data as blocks across cluster nodes.
* Provides fault tolerance and high throughput.
* Other components (Hive, Impala, Spark, HBase) read/write from it.

---

## 🧮 Data Processing and Query Engines

### 🐝 Hive

* SQL interface for data stored in HDFS.
* Converts queries into MapReduce / Tez / Spark jobs for batch processing.
* Ideal for ETL and large-scale aggregations.
* Defines table metadata in the Hive Metastore.

### ⚡ Impala

* Real-time SQL query engine.
* Reads the same tables defined in Hive Metastore.
* Executes queries directly in memory for low-latency analytics.
* Best for BI dashboards and interactive analysis.

### 🔥 Spark / PySpark

* Distributed computation engine for batch, streaming, and ML.
* **PySpark** provides a Python API for Spark.
* Can read/write from:

  * HDFS
  * Hive tables
  * Iceberg tables
  * Parquet/ORC files
* Often used for ETL, data transformation, or feature engineering.

### 🕒 Oozie

* Orchestrates complex workflows and schedules recurring jobs in the Hadoop ecosystem.
* Coordinates jobs such as Hive scripts, Spark jobs, shell commands, HDFS actions.
* Enables dependency management, error-handling, and scheduling (time or data triggers).

---

## 🧊 Iceberg — Modern Table Format

**Apache Iceberg** improves upon Hive’s traditional table format.

✅ **Features:**

* ACID transactions
* Schema evolution (add/remove columns safely)
* Hidden partitioning
* Time travel (query older snapshots)

**Integration:**

* Stored on HDFS or cloud storage.
* Accessible via Hive, Spark, Impala, Presto, etc.

---

## 🗂 File Formats — Parquet vs ORC

| Feature           | Parquet                      | ORC                                            |
| ----------------- | ---------------------------- | ---------------------------------------------- |
| Type              | Columnar                     | Columnar                                       |
| Developed By      | Twitter & Cloudera           | Hortonworks                                    |
| Optimized For     | Spark, Impala, Iceberg       | Hive, Spark                                    |
| Compression       | Snappy, GZIP, LZO, ZSTD      | ZLIB, Snappy                                   |
| Read Performance  | Excellent for Spark & Impala | Excellent for Hive                             |
| Write Performance | Faster                       | Slower, but better compression                 |
| Metadata          | Stored per column chunk      | Rich stats per stripe (min/max, bloom filters) |
| File Extension    | `.parquet`                   | `.orc`                                         |

**Example:**

```python
# PySpark Example
df = spark.read.csv("data.csv", header=True)
df.write.parquet("data_parquet/")
df.write.orc("data_orc/")
```

---

## 🧰 HBase — NoSQL Real-time Store

* Built on HDFS but optimized for **random read/write**.
* Schema-flexible: stores data as key-value pairs.
* Suitable for:

  * IoT sensor data
  * Time-series logs
  * Real-time lookup tables
* Accessible via:

  * APIs (Java, Python, REST)
  * Apache Phoenix for SQL queries
  * Hue HBase Browser

---

## 🏢 Teradata — Enterprise Data Warehouse

* Highly scalable MPP (Massively Parallel Processing) SQL data warehouse for large-scale structured analytics.
* Often used as the **enterprise “single source of truth”** for curated, cleaned data.
* Works alongside Hadoop ecosystems:

  * Raw data processed in Hadoop → summaries/load to Teradata
  * BI tools connect to Teradata for stable reporting.
* Architecture highlights:

  * Shared-nothing architecture
  * Parsing Engine (PE) for SQL queries
  * AMP (Access Module Processor) nodes for parallel data processing
  * BYNET network for high-speed inter-node communication

---

## 🖥️ Hue — The User Interface Layer

**Hue (Hadoop User Experience)** provides a web-based UI for:

* Writing and running Hive or Impala SQL queries.
* Browsing and managing HDFS files.
* Viewing HBase tables.
* Managing Spark jobs and workflows (including Oozie workflows).

---

## ⚙️ Example End-to-End Workflow

1. Data lands in **HDFS** from logs or ingestion.
2. **Oozie** triggers jobs (e.g., nightly at 02:00).
3. **PySpark** cleans and transforms the data, writes output to **Iceberg/Hive tables**.
4. Results are stored in **Parquet or ORC** format.
5. **Hive** runs scheduled ETL aggregations.
6. **Impala** enables interactive analytics on that data.
7. **Teradata** receives curated, structured data for enterprise reporting.
8. **HBase** serves real-time data lookups or time-series.
9. **Hue** is used by analysts/engineers to run queries, monitor jobs, browse data, and visualize results.

---

## 🚀 Summary

| Layer          | Technology      | Role                                                    |
| -------------- | --------------- | ------------------------------------------------------- |
| UI             | Hue             | Web-based UI for querying and data exploration          |
| Schedule       | Oozie           | Orchestrates and schedules workflows in Hadoop          |
| SQL Engines    | Hive / Impala   | Batch and interactive SQL processing                    |
| Processing     | Spark / PySpark | Distributed data processing & ETL                       |
| Storage Format | Iceberg         | Table management with ACID and schema evolution         |
| File Formats   | Parquet / ORC   | Compressed columnar storage for analytics               |
| Storage        | HDFS            | Distributed, fault-tolerant storage layer               |
| NoSQL          | HBase           | Real-time read/write data store                         |
| DW             | Teradata        | Enterprise data warehouse for large-scale SQL analytics |

---

## 🧠 Quick Summary in One Line

> **HDFS** stores → **Iceberg/Hive** organize → **Impala/Hive** analyze → **PySpark** processes → **HBase** serves real‐time → **Teradata** warehouses curated data → **Oozie** orchestrates the jobs → **Hue** visualizes and manages it all.


