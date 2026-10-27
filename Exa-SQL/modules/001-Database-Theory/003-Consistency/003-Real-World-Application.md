
## Database Consistency

Imagine working at the Pennsylvania DMV and you've been asked to work on the database for the new Driver's License. Due to growing population sizes, they've required a new driver's license number to help identify individuals. Your team has determined that every individuals driver's license number must include the following: 1 Alpha + 6 Numerics + 1 Alpha. All driver license numbers are now required to follow this rule, such that "P123456A" is a valid entry consistent with the format mentioned. Any entry that doesn't fit those stipulations, such as "P12345678", would result in error for inconsistent data as it's format is 1 Alpha + 8 Numerics.

## Database Inconsistency

Keeping with the driver's license example, imagine a driver's home address changes. This update must be represented across all tables where that prior address existed. If any table contains the old address, but others contain the new address for the driver would be a prime example of database inconsistency.