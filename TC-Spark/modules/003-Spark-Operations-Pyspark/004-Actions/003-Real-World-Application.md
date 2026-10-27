### Scenario: Server Log Analysis

An organization processes large volumes of server logs stored in
distributed storage.

Engineers may need to:

-   Count total log entries.
-   Retrieve a sample record for validation.
-   Aggregate error counts.
-   Save processed logs back to storage.

Example:

``` python
logs = sc.textFile("/data/server_logs.txt")

# Total log count
total_logs = logs.count()

# First log entry
first_log = logs.first()

# Count error logs
error_count = logs.filter(lambda x: "ERROR" in x).count()
```

In this scenario:

-   `count()` measures system activity.
-   `first()` validates log structure.
-   `filter().count()` helps detect system issues.
-   `collect()` is used carefully for small debugging samples.

Actions make distributed computations visible and usable at the driver
level.