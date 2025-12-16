
## 📘 **End-to-End Execution Flow of a Spark Job Triggered From Hue (Using Oozie)**

### 1. 🎛️ Submitting a Spark Job From Hue

When you open Hue → **Oozie → Workflow Editor → Spark Action**, you define:

* **Spark program type** (Hue may call all Spark jobs “Spark Program”, even Python)
* **Main file** (Python `.py` or JAR)
* **Files/Archives** to ship
* **Arguments**
* **Spark master** (e.g., `yarn`)
* **Configuration properties**

When you click **Run**, Hue:

1. Generates an internal `workflow.xml`.
2. Uploads all referenced files into an HDFS workflow directory:

```

/user/<username>/oozie/workflows/<workflow-id>/

```
3. Submits the job to **Oozie**.

---

### 2. 📡 What Oozie Does After Hue Submits the Workflow

Oozie:

1. Loads the workflow definition from HDFS.
2. Validates required files:

* `workflow.xml`
* Python script or JAR
* Additional files listed in `<file>` tags
3. Creates an internal workflow instance with:

* Job ID
* Execution DAG
* Spark action metadata

Oozie now governs the entire execution.

---

### 3. 🚀 When the Workflow Reaches the Spark Action

Oozie launches a **Spark Launcher Job** on YARN.

The launcher job:

1. Localizes (downloads) all workflow files:

* Python script
* JAR (if present)
* Additional files (CSV, JSON, config)
2. Prepares a **spark-submit** command based on:

* Your “Jar/py” field
* Any Spark config or args
* YARN mode

Oozie builds the **exact spark-submit command** — not Hue.

---

### 4. 🧳 How Files Are Shipped to YARN Nodes

#### Python Spark Job (`.py`)

Oozie sends:

* The `.py` file defined in **Jar/py name**
* Anything listed under:

* **Files**
* **Archives**

YARN localizes them into:

```

/mnt/yarn/container-executor/<job-id>/

```

Your Python script is now physically present on:

* The launcher container
* The executor containers

#### JAR Spark Job

Oozie ships the JAR + any dependencies similarly.

---

### 5. 🧾 How Oozie Builds the spark-submit Command

#### For Python:

```

spark-submit 
--master yarn 
--deploy-mode cluster 
--files top_10.py 
top_10.py 
arg1 arg2 arg3

```

#### For JAR:

```

spark-submit 
--class com.example.Main 
--master yarn 
--deploy-mode cluster 
my_spark_app.jar 
arg1 arg2

````

Important:
**Hue labels don’t matter.
Oozie decides whether it’s Python or JAR based ONLY on your Spark action config.**

---

### 6. ⚠️ Spark-Python Version Check (Potential Issue)

Before the Spark job fully starts:

* The Python interpreter used in the driver/executor containers **must match the PySpark version** installed on the cluster.
* **Mismatch symptoms:**
  - `TypeError: code expected at least 16 arguments, got 15`
  - `AttributeError` or `ImportError` due to incompatible PySpark APIs
* Happens **inside YARN executor/driver containers**, not Hue.
* Fix:
  - Verify versions:
    ```bash
    python --version
    pip show pyspark
    ```
  - Align Python and PySpark versions across cluster nodes.

---

### 7. 🧵 YARN Executes the Spark Job

YARN allocates:

* **ApplicationMaster** → Spark Driver
* **Executor containers** → Parallel computation workers

For Python jobs:

```

python top_10.py --args...

```

For JAR jobs:

```

java -cp myapp.jar com.example.MainClass

```

Your SparkSession starts, reads Hive tables, Parquet files, etc.

---

### 8. 🧩 Reading Hive/Impala Tables in Spark

Spark uses the **Hive Metastore** to resolve:

* Column names
* Types
* Partitions
* File locations

Spark does **not** talk to Impala directly; it reads Parquet ORC files from HDFS using the schema from Hive.

---

### 9. 📝 Logging and Status Monitoring

Hue shows:

* Spark stdout/stderr logs
* YARN container logs
* ApplicationMaster logs
* Each executor’s logs

Hue doesn’t execute Spark — it only polls Oozie and YARN.

---

### 10. ✔ How Parameter Passing Works

#### Steps to pass parameters in Hue:

#### 1️⃣ Define in “Parameters” panel:

```

table_name = granite_bond_price_ejv_stg
top_n = 10

```

#### 2️⃣ In Spark action → Arguments:

```

${table_name}
${top_n}

````

#### 3️⃣ In Python script:

```python
import sys

table_name = sys.argv[1]
top_n = int(sys.argv[2])
````

The arguments appear to Spark exactly in order.

---

### 11. 🔁 After Spark Completes

1. Driver exits with success/failed code.
2. Oozie reads the exit code.
3. Workflow moves to:

   * Next node (success)
   * Error handler node (failure)

---

### 12. 🧹 Cleanup

After the workflow finishes:

* YARN releases containers
* Localized temporary files are deleted
* Oozie job directory is retained only for retention period (for audit/logging)

---

### 13. ✔ Full Lifecycle Summary Diagram

```
Hue 
 → submits workflow to Oozie 
   → Oozie launches Spark action 
     → YARN starts Spark Launcher 
       → spark-submit is executed 
         → Driver + Executors run your .py/.jar 
           → Spark reads Hive/HDFS 
             → Spark job completes 
               → Status returned to Oozie 
                 → Hue shows final result
```
