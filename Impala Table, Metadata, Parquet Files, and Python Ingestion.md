## Impala Table, Metadata, Parquet Files, and Python Ingestion:

This document provides a structured view of how Impala interacts with Parquet files, how metadata is maintained, how Python-written Parquet files fit into the ecosystem, and how operations like REFRESH and INVALIDATE METADATA affect visibility and schema validation.

---

## 1. Impala Table Creation and Metadata Model

An Impala table is defined using Hive Metastore metadata. A typical DDL looks like:

```sql
CREATE TABLE sales (
  id BIGINT,
  amount DOUBLE,
  description STRING
)
PARTITIONED BY (cob_dt STRING)
STORED AS PARQUET;
```

When this DDL runs:

* Only logical metadata is created.
* No data files are generated.
* Column order, column names, and data types become the authoritative schema.
* The table’s storage location (default or custom) is registered.

Impala uses the metastore to understand table structure, but it does not enforce type consistency until data is read.

---

## 2. Parquet File Structure and Schema

A Parquet file contains:

* Column names.
* Physical storage types (INT32, INT64, BYTE_ARRAY UTF8, etc.).
* Encodings and metadata.

Each Parquet file stores its schema internally. There is no shared global schema registry. Impala verifies compatibility by comparing the file footer schema with the metastore schema when the file is scanned.

---

## 3. Writing Parquet Files Using Python

When Python writes a Parquet file (pyarrow, fastparquet, pandas):

```python
import pyarrow as pa
import pyarrow.parquet as pq

schema = pa.schema([
    ("id", pa.int64()),
    ("amount", pa.float64()),
    ("description", pa.string())
])

table = pa.Table.from_pandas(df, schema=schema)
pq.write_table(table, "/path/to/file.parquet")
```

Important properties:

* Python writers do not know the Impala table schema.
* They generate whatever schema the DataFrame and Python types dictate.
* No errors occur at write time for mismatches with Impala.
* The resulting Parquet file may or may not be compatible with the Impala table schema.

Therefore, explicit schema enforcement is required if type safety matters.

---

## 4. Loading Python-Written Files into Impala

### Adding Files to a Partition Directory

Placing a file under:

```
/warehouse/tablespace/managed/hive/sales/cob_dt=2025-01-01/
```

makes it an implicit part of that Impala partition.

Impala does not detect new files immediately unless REFRESH or automatic metadata refresh occurs.

---

## 5. How Impala Validates Parquet Schema

Impala performs schema validation **when reading a file**. The steps:

1. The query determines which partitions to scan.
2. Impala reads the Parquet file footer.
3. Impala compares each column’s physical type with the table schema.
4. If incompatible, Impala throws an error, such as:

```
Incompatible Parquet schema in file ...
```

Validation is not performed at the time the file is written or when it is first discovered by the catalog.

---

## 6. REFRESH and INVALIDATE METADATA

### REFRESH

```sql
REFRESH sales;
```

Characteristics:

* Updates file listings for the table.
* Causes Impala to discover new or replaced Parquet files.
* Does not clear metastore metadata.
* Does not validate schema.
* File schema mismatch will appear only when files are queried.

Use REFRESH when:

* Python inserts new Parquet files.
* Existing data files are updated or replaced.
* New partitions appear that already exist in the metastore.

### INVALIDATE METADATA

```sql
INVALIDATE METADATA sales;
```

Characteristics:

* Drops all cached metadata for that table.
* Forces a full reload from the Hive Metastore.
* Heavy operation compared to REFRESH.
* Required when structural metadata changes, such as:

  * Column type changes.
  * Column additions/removals.
  * Partition addition through external tools that update the metastore.

Invalidating does not fix schema mismatch between Parquet files and tables. It only resets metadata awareness.

---

## 7. Behavior with Multiple Parquet Files and Mixed Schemas

If some files have matching schema and others do not:

* Queries scanning only matching partitions succeed.
* Queries scanning partitions containing mismatched files fail.
* Queries across the entire table also fail because Impala attempts to read all files.

Example:

```
Partition 1 (good)    -> OK
Partition 2 (good)    -> OK
Partition 3 (bad)     -> schema mismatch error when scanned
```

Impala validates each file independently but only when needed.

---

## 8. Practical Schema Enforcement Workflow

To ensure consistent ingestion:

1. Retrieve Impala schema from Hive Metastore or a predefined source.
2. Cast or convert DataFrame columns to corresponding Python types.
3. Define an explicit pyarrow schema.
4. Write Parquet files with that schema.
5. Move files into Impala partition location.
6. Run `REFRESH` to register new files.
7. Query the partition and validate.

This avoids runtime failures caused by Parquet schema inconsistencies.

---

## 9. Summary

* Impala stores only logical metadata; Parquet files store physical schema.
* Python-written Parquet files must match the Impala schema exactly.
* REFRESH brings new files into Impala’s visibility but does not validate schema.
* INVALIDATE METADATA reloads structural metadata but does not fix mismatches.
* Schema mismatch errors occur only when a query attempts to read the mismatched file.
* Only partitions containing mismatched files trigger errors during scans.
* Explicit schema enforcement in Python is essential for reliable ingestion.

If you want, I can extend this into an operational checklist or provide sample Python code that self-validates against Impala before writing.
