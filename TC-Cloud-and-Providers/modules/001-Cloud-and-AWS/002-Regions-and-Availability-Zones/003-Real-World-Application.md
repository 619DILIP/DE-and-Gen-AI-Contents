## Designing for Geography and Failure

A company serving customers primarily in Europe would normally run its workloads in a European region. The latency is lower for those users, and data protection rules may require personal data to remain within the region regardless of any other consideration.

Within that region, anything that needs to stay available is distributed across availability zones. The application servers are spread across at least two, and the database runs with a standby in a second zone. A single zone becoming unavailable degrades capacity rather than stopping the service.

Separately, backups are often replicated to a second region. Availability zones protect against the loss of a data center; a second region protects against a problem affecting an entire geographic area. The two serve different purposes, and a design concerned with continuity usually accounts for both.