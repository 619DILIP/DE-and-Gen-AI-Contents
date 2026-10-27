## 1. Word Count System

- Convert words into (word, 1)
- Use reduceByKey() to count occurrences
- Save aggregated results

---

## 2. Log Analytics

- Extract (error_code, 1)
- Use reduceByKey() to count error frequency
- Use sortByKey() to organize logs

---

## 3. Sales Aggregation

- Create (product_id, sale_amount)
- Use aggregateByKey() to compute total revenue
- Use keys() to get unique product IDs

---

## 4. Data Sampling

- Use sampleByKey() to analyze subset of large datasets

Efficient key-based transformations are critical in distributed systems
where aggregation is common.