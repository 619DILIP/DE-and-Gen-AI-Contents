## Getting Data Into a Warehouse

Data does not arrive in a data warehouse on its own. It has to be extracted from source systems, transformed into the correct structure, and loaded into its final destination. ETL and ELT are two different orderings of this same basic process, and the difference between them has real consequences for performance and system design.

---

## ETL: Extract, Transform, Load

ETL performs these three steps in order:

1. **Extract**: Pull raw data out of source systems, such as an application database or an external file.
2. **Transform**: Clean, reshape, and standardize that data, for example converting date formats, removing duplicates, or joining data from multiple sources, all before it is loaded anywhere permanent.
3. **Load**: Write the finished, transformed data into the destination warehouse.

```text
Source Data → Extract → Transform (in a separate processing system) → Load → Warehouse
```

The key detail in ETL is that transformation happens outside the warehouse, in a separate processing system, before the data ever touches its final destination. This was the standard approach for decades, largely because older warehouse systems were not powerful enough to handle heavy transformation work themselves.

---

## ELT: Extract, Load, Transform

ELT reorders the last two steps:

1. **Extract**: Pull raw data out of source systems, exactly as in ETL.
2. **Load**: Load that raw, untransformed data directly into the warehouse first.
3. **Transform**: Perform the cleaning and reshaping afterward, using the processing power of the warehouse itself.

```text
Source Data → Extract → Load (raw data goes straight into the warehouse) → Transform (inside the warehouse)
```

ELT became practical as modern cloud data warehouses, such as Snowflake, Redshift, and BigQuery covered earlier, grew powerful enough to handle large scale transformation work directly, removing the need for a separate transformation system.

---

## Why the Order Matters

| | ETL | ELT |
|---|---|---|
| Where transformation happens | Separate processing system, before loading | Inside the warehouse, after loading |
| Raw data availability | Not stored, only transformed data is loaded | Raw data is available in the warehouse alongside transformed data |
| Flexibility | Transformation logic must be decided upfront | Transformation logic can be changed or reapplied later, since raw data is retained |
| Infrastructure needs | Requires a separate transformation system | Relies on the compute power of the warehouse itself |

Because ELT retains the raw data inside the warehouse, it offers more flexibility. If a business requirement changes and a different transformation is needed, that transformation can be rerun against the raw data already sitting in the warehouse, rather than needing to re extract everything from the original source systems again.

---

## Choosing Between ETL and ELT

ETL remains a reasonable choice when source data needs significant cleaning or sensitive data needs to be filtered or masked before it ever reaches the warehouse, for compliance or security reasons. ELT is generally favored in modern cloud environments where the warehouse itself has ample compute power, and where retaining raw data provides useful flexibility for future analysis.
