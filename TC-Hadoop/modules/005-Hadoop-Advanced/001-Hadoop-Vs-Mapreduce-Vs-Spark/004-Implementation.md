## 1️⃣ Hadoop MapReduce (Python via Hadoop Streaming)

### Mapper (mapper.py)

``` python
#!/usr/bin/env python
import sys

for line in sys.stdin:
    words = line.strip().split()
    for word in words:
        print(f"{word}\t1")
```

### Reducer (reducer.py)

``` python
#!/usr/bin/env python
import sys
from itertools import groupby
from operator import itemgetter

def read_mapper_output(file, separator='\t'):
    for line in file:
        yield line.rstrip().split(separator, 1)

data = read_mapper_output(sys.stdin)

for current_word, group in groupby(data, itemgetter(0)):
    try:
        total_count = sum(int(count) for _, count in group)
        print(f"{current_word}\t{total_count}")
    except ValueError:
        pass
```

### Execution

``` bash
hadoop jar hadoop-streaming.jar \
-input input.txt \
-output output \
-mapper mapper.py \
-reducer reducer.py
```

------------------------------------------------------------------------

## 2️⃣ Apache Spark (PySpark)

``` python
from pyspark.sql import SparkSession

spark = SparkSession.builder.appName("WordCount").getOrCreate()

text_file = spark.read.text("input.txt")

words = text_file.rdd.flatMap(lambda line: line.value.split())

word_counts = words.map(lambda word: (word, 1)).reduceByKey(lambda a, b: a + b)

word_counts.saveAsTextFile("output")

spark.stop()
```

### Execution

``` bash
spark-submit wordcount.py
```

------------------------------------------------------------------------

## Key Implementation Differences

| Aspect                | MapReduce                     | Spark            |
|------------------------|--------------------------------|------------------|
| Code Structure         | Separate mapper & reducer      | Single script    |
| Intermediate Data      | Written to disk                | Stored in memory |
| Development Speed      | Slower                         | Faster           |
| Iterative Processing   | Inefficient                    | Efficient        |
