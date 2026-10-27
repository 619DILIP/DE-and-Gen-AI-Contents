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