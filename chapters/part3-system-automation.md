[← Part 2 – Text, Files, and Data Cleaning](part2-text-files-data-cleaning.md) · [Home](../README.md) · [Next → Part 4 – Databases & ETL](part4-databases-etl.md)
---

# Part 3 – System Automation & Integration

## 10. System Automation Toolkit

Use `os`, `pathlib`, `shutil`, and `subprocess` for system automation.

```python
import os
import shutil
import subprocess
from pathlib import Path

token = os.getenv("API_TOKEN")

shutil.copy("src.txt", "backup/")
result = subprocess.run(
    ["ls", "-l"],
    capture_output=True,
    text=True,
    check=True,
)
print(result.stdout)
```

## 11. CLI Tools with argparse

```python
import argparse

def parse_args():
    p = argparse.ArgumentParser(description="Process logs")
    p.add_argument("input")
    p.add_argument("output")
    p.add_argument("-v", "--verbose", action="count", default=0)
    p.add_argument("--dry-run", action="store_true")
    return p.parse_args()
```

## 12. Working with HTTP & APIs

```python
import time
import requests

def get_with_retry(url: str, retries: int = 3, delay: float = 1.0):
    for i in range(retries):
        try:
            resp = requests.get(url, timeout=10)
            resp.raise_for_status()
            return resp
        except Exception:
            if i == retries - 1:
                raise
            time.sleep(delay * (2 ** i))
```

## 13. Schedulers, Jobs, and Script Runners

- Cron jobs on Linux/WSL
- Windows Task Scheduler
- Lightweight Python job loops for simple repeating tasks
