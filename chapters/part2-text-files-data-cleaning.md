[← Part 1 – Core Language](part1-core-language.md) · [Home](../README.md) · [Next → Part 3 – System Automation & Integration](part3-system-automation.md)
---

# Part 2 – Text, Files, and Data Cleaning

## 6. Strings & Regex

String normalization:

```python
s = "  ERROR 503 Service Unavailable  "
clean = " ".join(s.strip().split())
```

Regular expressions (`re`):

```python
import re

if re.search(r"ERROR \d{3}", line):
    handle_error(line)

m = re.match(r"(\S+) - - \[(.*?)\] "(.*?)" (\d{3})", line)
if m:
    ip, timestamp, request, status = m.groups()
```

## 7. Files, Paths, Encodings

Use `pathlib.Path` everywhere:

```python
from pathlib import Path

p = Path("data") / "input.csv"
text = p.read_text(encoding="utf-8")
Path("output.txt").write_text("hello\n", encoding="utf-8")

for f in Path("logs").rglob("*.log"):
    print(f, f.stat().st_size)
```

## 8. JSON, CSV, YAML

JSON:

```python
import json
from pathlib import Path

data = json.loads(Path("input.json").read_text())
Path("out.json").write_text(json.dumps(data, indent=2, sort_keys=True))
```

CSV:

```python
import csv

with open("users.csv", newline="", encoding="utf-8") as f:
    for row in csv.DictReader(f):
        print(row["name"])
```

(YAML as needed for configs, e.g. with `pyyaml`.)

## 9. Data-Cleanup Engine Pattern

Normalization:

```python
def normalize(row: dict) -> dict:
    return {
        "id": row["ID"].strip(),
        "email": row["Email"].strip().lower(),
        "ts": row["Timestamp"].strip(),
    }
```

Validation + split:

```python
def is_valid(row: dict) -> bool:
    return row["id"] and "@" in row["email"]

good: list[dict] = []
bad: list[dict] = []

for row in map(normalize, rows):
    (good if is_valid(row) else bad).append(row)
```
