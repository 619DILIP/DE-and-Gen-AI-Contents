## Hadoop MapReduce Use Case

Imagine you have 10 large datasets (bags of data).  
Each mapper processes one dataset in parallel.  
The reducer aggregates the results.

Used for:
- Daily ETL jobs
- Log aggregation
- Data warehousing batch tasks

Industries:
- Banking
- Telecom
- Government archives

---

## Apache Spark Use Case

Spark is used when real-time speed matters.

Example:
- Real-time fraud detection
- Recommendation systems
- Live dashboard analytics
- Streaming analytics

Industries:
- E-commerce
- FinTech
- Media platforms
- Machine learning pipelines

---

## When to Choose What?

Choose MapReduce when:
- Processing large historical batch datasets
- Budget constraints exist
- Simpler batch pipeline required

Choose Spark when:
- Low latency is required
- Machine learning needed
- Interactive analytics required
- Real-time streaming required