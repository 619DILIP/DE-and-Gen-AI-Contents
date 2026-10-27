## 1. Interactive Analytics

Data scientists frequently use collect() or show(). If driver memory is
insufficient → crashes.

Solution: Increase spark.driver.memory.

---

## 2. Machine Learning Model Training

Driver coordinates iterative training. Large metadata and model states
stored in driver.

Solution: Increase driver memory and cores.

---

## 3. Large Broadcast Variables

Broadcasting large datasets from driver to executors requires sufficient
driver memory.

---

## 4. Streaming Applications

Driver handles micro-batch scheduling. Under-provisioned driver →
scheduling delays.

---