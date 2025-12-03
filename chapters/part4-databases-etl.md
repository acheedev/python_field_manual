[← Part 3 – System Automation & Integration](part3-system-automation.md) · [Home](../README.md) · [Next → Part 5 – Quality Layer](part5-quality-layer.md)
---

# Part 4 – Databases & ETL

## 14. DB-API Patterns

```python
import sqlite3

conn = sqlite3.connect(":memory:")

def query(conn, sql: str, params=None):
    with conn.cursor() as cur:
        cur.execute(sql, params or [])
        return cur.fetchall()

rows = query(conn, "SELECT 1")
```

## 15. SQLite for ETL & Testing

```python
conn = sqlite3.connect(":memory:")
conn.execute("CREATE TABLE users (id TEXT, email TEXT, ts TEXT)")
conn.executemany(
    "INSERT INTO users VALUES (?, ?, ?)",
    [(r["id"], r["email"], r["ts"]) for r in clean_rows],
)
conn.commit()
```

## 16. Postgres Integration

```python
import psycopg

with psycopg.connect("postgres://user:pass@localhost/db") as conn:
    with conn.cursor() as cur:
        cur.execute("SELECT id, name FROM users WHERE active=%s", (True,))
        rows = cur.fetchall()
```

## 17. Oracle Integration

```python
import oracledb

conn = oracledb.connect(user="scott", password="tiger", dsn="localhost/XEPDB1")
cur = conn.cursor()
cur.execute("BEGIN do_something(:id); END;", {"id": 123})
conn.commit()
```

## 18. ETL Pipeline Pattern

```python
def run_pipeline(csv_path, conn):
    extracted = extract_csv(csv_path)
    transformed = (transform(r) for r in extracted)
    good, bad = split(transformed)

    load_sqlite(conn, good)
    write_bad_csv("bad.csv", bad)
```

Replace `extract_csv`, `transform`, `split`, `load_sqlite`, and `write_bad_csv` with your concrete implementations.
