## What Is S3?

Amazon Simple Storage Service, known as S3, is AWS's object storage service. Unlike RDS, which stores structured data in database tables, S3 stores files, called objects, in a flat storage structure without requiring any predefined schema. This makes it well suited to storing data in any format, structured, semi structured, or unstructured, which connects directly to the data lake concept covered earlier.

---

## Buckets and Objects

S3 storage is organized around two core concepts:

- **Buckets**: Top level containers that hold objects. A bucket name must be globally unique across all of AWS, since bucket names form part of the resulting storage address.
- **Objects**: The individual files stored within a bucket, along with metadata describing them. An object can be nearly any file type: a CSV file, a JSON file, an image, a video, or a compressed archive.

```text
Bucket: company-sales-data
    ├── raw/2024-01-15/orders.csv
    ├── raw/2024-01-16/orders.csv
    └── processed/summary.json
```

Although S3 does not have real folders in the traditional sense, object names commonly include forward slashes, which most tools and the AWS console display as a folder like structure for organizational convenience.

---

## Common Use Cases

S3 is widely used for:

- **Raw data storage**: Holding unprocessed data as it arrives from various sources, before it is cleaned and loaded into a warehouse.
- **Data lake storage**: Serving as the underlying storage layer for a data lake, given its low cost and support for any file format.
- **Backups and archives**: Storing backup copies of data or systems for long term retention.
- **Static file hosting**: Serving files directly, such as website assets or downloadable reports.

Within a data pipeline, S3 is commonly the landing zone where raw extracted data is written first, before a transformation process reads it, cleans it, and loads it into a database such as RDS or a dedicated data warehouse platform.

---

## Access Control

Access to S3 buckets and objects is controlled through a combination of bucket policies and IAM permissions, the latter covered in more detail in the next module. By default, a newly created S3 bucket is private, accessible only to the AWS account that created it. Public access must be explicitly granted, and AWS provides safeguards specifically designed to prevent buckets from being made public accidentally, since misconfigured public buckets have historically been a common source of data exposure.

---

## Cost Characteristics

S3 is priced based on the amount of data stored, the number of requests made against it, and the amount of data transferred out of it. Because storage cost per unit is relatively low compared to a structured database, S3 is a natural fit for storing large volumes of raw or infrequently accessed data.