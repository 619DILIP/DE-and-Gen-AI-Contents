## Serving Warehouse Data

A common pattern places an API in front of a data warehouse. The warehouse holds aggregated sales figures, and several consumers need them: an internal dashboard, a partner's system, and a mobile application.

Rather than granting each consumer direct database access, a small API exposes a handful of endpoints such as:

* Revenue by region
* Revenue by month
* Product performance
* Customer summaries

That arrangement means database credentials are held in one place, access can be logged and rate limited, the query logic is written once rather than reimplemented by each consumer, and the underlying warehouse can be changed or migrated without each consumer needing to know.

The same skill applies in reverse during extraction. Pulling data from an external source frequently means consuming that source's API, and having built one makes reading someone else's API documentation considerably easier.