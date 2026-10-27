## Example: Word Count using Hadoop Streaming

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

### Execution Command

``` bash
hadoop jar hadoop-streaming.jar \
-input input.txt \
-output output \
-mapper mapper.py \
-reducer reducer.py
```

### Execution Flow

1.  Input file stored in HDFS
2.  Hadoop splits the file
3.  Mapper processes each split
4.  Shuffle groups identical keys
5.  Reducer aggregates results
6.  Output stored in HDFS