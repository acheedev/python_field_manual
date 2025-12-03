[← Part 0 – Setup](part0-setup-muscle-memory.md) · [Home](../README.md) · [Next → Part 2 – Text, Files, and Data Cleaning](part2-text-files-data-cleaning.md)
---

# Part 1 – Core Language

## 1. Names, Objects, Execution Model

Python binds **names** to **objects**. Assignment moves the *name*, not the underlying object.

```python
x = 5
y = x
x = 10  # y still refers to 5
```

Functions are objects:

```python
def greet():
    print("hi")

f = greet
f()  # calls greet
```

## 2. Control Flow & Exceptions

Basic branching:

```python
if n > 100:
    ...
elif n > 50:
    ...
else:
    ...
```

Exceptions are how Python signals errors:

```python
try:
    do_work()
except FileNotFoundError:
    LOG.error("Missing file")
except Exception as e:
    LOG.exception("Unexpected error: %s", e)
```

### Retry helper

```python
import time

def retry(fn, attempts: int = 3, delay: float = 1.0):
    for i in range(attempts):
        try:
            return fn()
        except Exception:
            if i == attempts - 1:
                raise
            time.sleep(delay)
```

## 3. Collections & Core Types

Lists, dicts, sets, and tuples are your bread and butter.

```python
nums = [1, 2, 3]
squares = [x * x for x in nums]
```

```python
from collections import defaultdict, Counter

groups = defaultdict(list)
groups["errors"].append("timeout")

counts = Counter(["a", "b", "a"])
```

## 4. Functions, Modules, and Type Hints

```python
def add(a: int, b: int = 0) -> int:
    return a + b
```

Modules:

```python
# project/lib/helpers.py
def parse_config(path):
    ...

# project/scripts/myscript.py
from lib.helpers import parse_config
```

## 5. Generators & Streaming

Generators let you stream data without loading everything into memory.

```python
def read_lines(path):
    with open(path) as f:
        for line in f:
            yield line.rstrip()
```

```python
def parse(line: str) -> dict:
    ts, msg = line.split(" ", 1)
    return {"timestamp": ts, "message": msg}

records = (parse(line) for line in read_lines("app.log"))
```
