In this module, we learned:

- A star schema connects a fact table to fully denormalized, flat dimension tables.
- A snowflake schema normalizes dimension tables into related tables to reduce redundancy.
- Star schemas generally offer simpler, faster queries, while snowflake schemas save storage space.
- The choice between them depends on the size of the dimensions and how much query performance matters relative to storage.
- Star schemas are the more common default in modern data warehouse design.

With schema design covered, the next topic shifts from how data is structured once it arrives in the warehouse to how it gets there in the first place, through ETL and ELT processes.
