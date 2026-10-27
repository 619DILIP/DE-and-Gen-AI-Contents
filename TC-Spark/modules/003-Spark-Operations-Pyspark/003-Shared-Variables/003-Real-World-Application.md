## Broadcast Variable Example

You have millions of transaction records and a small lookup dictionary
containing country codes.

Instead of sending the dictionary repeatedly to every task, you
broadcast it once to all executors.

Common uses:

-   Lookup tables
-   Configuration settings
-   Static reference data
-   Model parameters

## Accumulator Example

You are processing log files and need to count how many records contain
errors.

Each executor processes part of the data and increments an accumulator.
The driver retrieves the final aggregated count.

Common uses:

-   Counting invalid records
-   Monitoring job metrics
-   Debugging distributed tasks
-   Tracking statistics