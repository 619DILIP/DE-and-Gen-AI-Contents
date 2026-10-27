In this module, we learned:

- A region is an independent geographic area with its own AWS infrastructure, identified by a code such as `us-east-1`.
- Resources belong to a region, so the selected region determines what is visible, what it costs, and which services are available.
- Region choice is driven by latency, compliance and data residency requirements, and cost.
- An availability zone is one or more physically separate data centers within a region, with independent power and networking.
- Distributing resources across availability zones is how AWS workloads tolerate the failure of a single data center.
- Edge locations cache content close to users and are distinct from regions and availability zones, which run infrastructure.
- Region and zone choices are made at creation time and some are difficult to reverse, so they are worth deciding deliberately.

With the geographic structure understood, the next module looks at Amazon EC2, the virtual server service that most long running workloads use.