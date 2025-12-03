[← Part 6 – Tutoring Toolkit](part6-tutoring.md) · [Home](../README.md)
---

# Part 7 – Script Cookbook

This section is a library of ready-to-adapt script skeletons.

## Log Rotator (`rotate_logs.py`)

Rotates a log file, gzips older ones, keeps N backups.

```python
#!/usr/bin/env python3
"""Rotate and gzip log files, keeping N backups."""

# Full implementation in your scripts folder.
# Key ideas:
# - increment existing .N files
# - gzip older logs
# - keep only N backups
# - create a new empty active log file
```

## CSV Cleaner (`csv_quarantine_bad_rows.py`)

Split a CSV into `good.csv` and `bad.csv` based on validation rules.

```python
def is_valid(row: dict) -> bool:
    email = row.get("email", "").strip()
    id_ = row.get("id", "").strip()
    return bool(id_) and ("@" in email)
```

## API → SQLite Sync (`api_to_sqlite_sync.py`)

Fetch JSON from an API and upsert into a SQLite table.

```python
def upsert_items(conn, items: list[dict]):
    conn.executemany(
        """INSERT INTO items (id, name, updated_at)
               VALUES (:id, :name, :updated_at)
               ON CONFLICT(id) DO UPDATE SET
                   name=excluded.name,
                   updated_at=excluded.updated_at""",
        items,
    )
    conn.commit()
```

## SQL Report Generator (`run_sql_and_email_report.py`)

Run a SQL query, export results to CSV, and optionally email them.

## Directory Scanner (`scan_dir_summary.py`)

Scan a directory tree and report counts and sizes by extension.

```python
from collections import Counter, defaultdict
from pathlib import Path

def scan(root: Path):
    ext_counts = Counter()
    ext_sizes = defaultdict(int)
    total_files = 0
    total_size = 0

    for f in root.rglob("*"):
        if f.is_file():
            total_files += 1
            size = f.stat().st_size
            total_size += size
            ext = f.suffix.lower() or "<no-ext>"
            ext_counts[ext] += 1
            ext_sizes[ext] += size

    return total_files, total_size, ext_counts, ext_sizes
```

## URL Checker (`check_urls.py`)

Check HTTP status codes for a list of URLs.

## JSON → Oracle Loader (`json_to_oracle_loader.py`)

Load a JSON array of objects into an Oracle table using `executemany` and bind arrays.
