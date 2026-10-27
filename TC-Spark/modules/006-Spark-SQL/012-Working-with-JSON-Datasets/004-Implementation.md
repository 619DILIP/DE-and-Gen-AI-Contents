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