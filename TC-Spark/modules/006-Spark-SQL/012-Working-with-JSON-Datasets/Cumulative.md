<details><summary>Learning Objectives</summary>

After completing this module, learners should be able to:

- Read JSON files into Spark DataFrames
- Handle multiline JSON files
- Work with nested JSON structures
- Read multiple JSON files and directories
- Write DataFrames back to JSON format
- Use Spark SQL to query JSON data

</details>

<details><summary>Description</summary>

## Introduction to JSON in Spark

JSON (JavaScript Object Notation) is a widely used format for storing
and exchanging structured and semi-structured data.

Spark SQL can automatically:

- Infer the schema of JSON data
- Load JSON files into DataFrames
- Query nested fields
- Write DataFrames back to JSON format

---

## Reading JSON Files

Spark provides:

spark.read.json("path")

or

spark.read.format("json").load("path")

Spark automatically detects:

- Column names
- Data types
- Nested structures

---

## Multiline JSON

Some JSON files contain one record spread across multiple lines.

To read such files:

.option("multiline", "true")

---

## Reading Multiple Files

You can:

- Pass multiple file paths
- Pass a directory path
- Use wildcards like \*.json

---

## Working with Nested JSON

Spark allows access to nested fields using dot notation:

df.select("parent.child")

Nested arrays and structs are supported.

---

## Writing DataFrame to JSON

Use:

df.write.json("output_path")

You can specify:

- mode("overwrite")
- mode("append")
- mode("ignore")
- mode("error")

---

## Save Modes

- overwrite → Replaces existing data
- append → Adds new data
- ignore → Skips if path exists
- error → Throws error if path exists

---

## Important Options

- nullValue → Treat specific value as null
- dateFormat → Format date columns
- inferSchema → Automatically detect types

</details>

<details><summary>Real World Application</summary>

## 1. Log Analytics

Application logs are often stored in JSON format and analyzed using
Spark.

---

## 2. API Data Processing

Data fetched from REST APIs is typically JSON and can be directly loaded
into Spark.

---

## 3. IoT Data Streams

Sensor data in JSON format can be processed for analytics.

---

## 4. Data Lake Ingestion

JSON files stored in cloud storage are converted into structured
DataFrames.

---

## 5. Nested Event Processing

User activity events with nested fields can be queried using Spark SQL.

</details>

<details><summary>Implementation</summary>

## Step 1: Create SparkSession

```python
from pyspark.sql import SparkSession

spark = (
    SparkSession.builder
    .appName("JSONExample")
    .getOrCreate()
)
```

---

## Step 2: Read JSON File

```python
df = spark.read.json("zipcodes.json")
df.printSchema()
df.show(truncate=False)
```

---

## Step 3: Read Multiline JSON

```python
df_multiline = (
    spark.read
    .option("multiline", "true")
    .json("multiline_zipcodes.json")
)

df_multiline.show(truncate=False)
```

---

## Step 4: Read Multiple JSON Files

```python
df_multi = spark.read.json("data/zipcode1.json", "data/zipcode2.json")
df_multi.show()
```

Or read entire directory:

```python
df_dir = spark.read.json("data/json_folder/")
df_dir.show()
```

---

## Step 5: Access Nested Fields

```python
df.select("address.city").show()
```

---

## Step 6: Register Temporary View

```python
df.createOrReplaceTempView("zipcodes")
spark.sql("SELECT * FROM zipcodes").show()
```

---

## Step 7: Write DataFrame to JSON

```python
df.write.mode("overwrite").json("output/json_data")
```

---

## Step 8: Specify Options While Writing

```python
df.write   .mode("append")   .option("dateFormat", "yyyy-MM-dd")   .json("output/json_data")
```

---

## Step 9: Check Schema

```python
df.printSchema()
```

---

## Step 10: Show Data

```python
df.show()
```

</details>

<details><summary>Summary</summary>

In this module, we learned:

- Spark can automatically infer JSON schema
- JSON files can be read using spark.read.json()
- Multiline JSON requires multiline option
- Multiple files and directories can be loaded together
- Nested fields can be accessed directly
- DataFrames can be written back to JSON format
- Save modes control how data is written

Working with JSON is essential for handling semi-structured data in
modern data engineering workflows.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>
