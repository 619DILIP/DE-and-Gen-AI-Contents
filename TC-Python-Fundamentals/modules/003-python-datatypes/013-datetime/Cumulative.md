# Cumulative for datetime

<details><summary>Learning Objectives</summary>

# Learning Objectives
After completing this module, associates should be able to:

- Explain what the **`datetime`** module is and why Python uses it
- Create and manipulate `date`, `time`, and `datetime` objects
- Parse dates from strings and format datetime objects into readable text
- Perform date/time arithmetic (adding, subtracting, comparing)
- Use `timedelta` to represent time differences
- Handle common real-world patterns such as timestamps and time zones

</details>

<details><summary>Description</summary>

# What is `datetime`?

The **`datetime`** module is Python’s built-in library for working with dates, times, and timestamps.  
It includes several classes:

- **`date`** → represents a calendar date (year, month, day)
- **`time`** → represents a time of day (hour, minute, second)
- **`datetime`** → a full timestamp (date **and** time)
- **`timedelta`** → represents differences between two dates or times
- **`timezone`** → represents time zone information

Python does **not** store dates or times as strings — instead, it uses these well-defined objects to perform accurate arithmetic, comparisons, and formatting.

This module is used in virtually every real-world application involving logs, events, APIs, timestamps, or scheduling.

</details>

<details><summary>Real World Application</summary>

# Real World Application for `datetime`

The `datetime` module is used throughout real systems:

### ✔️ Logging & Audit Trails  
Timestamps in log files always use `datetime`.

### ✔️ APIs & Web Applications  
Track creation dates, last-updated timestamps, session expiration, etc.

### ✔️ Scheduling & Automation  
Cron jobs, reminders, ETL runs, and scheduled tasks are built using datetime math.

### ✔️ Data Engineering & ETL  
Parsing timestamps from CSVs, converting time zones, grouping by date, etc.

### ✔️ Finance & Analytics  
Interest calculations, trading timestamps, and daily/weekly aggregates.

### ✔️ Machine Learning  
Creating time-based features: hour-of-day, day-of-week, month-over-month deltas.

Understanding `datetime` is essential for all serious Python development.

</details>

<details><summary>Implementation</summary>

# Implementation

## Importing the module

You can import the entire module:

```python
import datetime
````

Or import specific classes:

```python
from datetime import date, time, datetime, timedelta
```

---

## Working With `date`

### Creating a date:

```python
from datetime import date

d = date(2025, 11, 15)
print(d)   # 2025-11-15
```

### Today's date:

```python
today = date.today()
```

### Accessing attributes:

```python
print(today.year)
print(today.month)
print(today.day)
```

---

## Working With `time`

```python
from datetime import time

t = time(14, 30, 0)
print(t.hour)   # 14
print(t.minute) # 30
```

---

## Working With `datetime`

### Current date + time:

```python
from datetime import datetime

now = datetime.now()
```

### Creating a specific datetime:

```python
dt = datetime(2025, 11, 15, 10, 45, 30)
```

### Extracting components:

```python
dt.year
dt.month
dt.hour
dt.minute
```

---

## Parsing & Formatting Dates

### Parsing strings → datetime (`strptime`)

```python
dt = datetime.strptime("2025-11-15 14:30", "%Y-%m-%d %H:%M")
```

### Formatting datetime → string (`strftime`)

```python
now.strftime("%B %d, %Y")     # 'November 15, 2025'
now.strftime("%Y/%m/%d %H:%M")
```

Common format codes:

| Code | Meaning         |
| ---- | --------------- |
| `%Y` | 4-digit year    |
| `%m` | 2-digit month   |
| `%d` | day of month    |
| `%H` | hour (24h)      |
| `%M` | minute          |
| `%S` | second          |
| `%B` | full month name |

---

## `timedelta` — Date Arithmetic

```python
from datetime import datetime, timedelta

now = datetime.now()
future = now + timedelta(days=7)
past = now - timedelta(hours=3)
```

Example:

```python
delta = future - now
print(delta.days)     # 7
```

---

## Comparing Dates & Times

```python
d1 = datetime(2025, 1, 1)
d2 = datetime(2025, 2, 1)

print(d1 < d2)   # True
```

---

## Time Zones (`timezone`)

Basic usage:

```python
from datetime import datetime, timezone, timedelta

utc = timezone.utc
dt = datetime.now(utc)
```

Creating custom offsets:

```python
est = timezone(timedelta(hours=-5))
local_dt = datetime.now(est)
```

---

## Converting Between Timestamps & Datetime

### Datetime → Unix timestamp

```python
timestamp = datetime.now().timestamp()
```

### Unix timestamp → datetime

```python
dt = datetime.fromtimestamp(timestamp)
```

This is extremely common in logs and APIs.

</details>

<details><summary>Summary</summary>

# Summary

* The **`datetime`** module provides classes for working with dates, times, and timestamps.
* `date`, `time`, and `datetime` represent different aspects of time-based data.
* `timedelta` allows arithmetic such as adding days or subtracting hours.
* `strftime` formats datetimes into strings; `strptime` parses strings into datetime objects.
* Time zone support is available through the `timezone` class.
* datetime operations appear in nearly all real-world Python applications involving logs, APIs, databases, ETL pipelines, automation, and analytics.

</details>

<details><summary>Practice Questions</summary>

[Practice Questions](./Quiz.gift)

</details>