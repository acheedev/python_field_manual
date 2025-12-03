[← Part 4 – Databases & ETL](part4-databases-etl.md) · [Home](../README.md) · [Next → Part 6 – Tutoring Toolkit](part6-tutoring.md)
---

# Part 5 – Quality Layer

## 19. Logging

```python
import logging
import sys

def setup_logging(verbosity: int = 0):
    level = logging.WARNING
    if verbosity == 1:
        level = logging.INFO
    elif verbosity >= 2:
        level = logging.DEBUG

    logging.basicConfig(
        level=level,
        format="%(asctime)s [%(levelname)s] %(name)s: %(message)s",
        handlers=[logging.StreamHandler(sys.stdout)],
    )
```

## 20. Testing

```python
def normalize_email(email: str) -> str:
    return email.strip().lower()

def test_normalize_email():
    assert normalize_email(" John@EXAMPLE.COM  ") == "john@example.com"
```

## 21. Type Hints

```python
from typing import TypedDict

class User(TypedDict):
    id: int
    email: str
    active: bool

def load_user(id: int) -> User:
    ...
```

## 22. Architecture & Design Patterns

- Pipeline pattern (extract → transform → load)
- Dependency injection (pass in DB, config, paths)
- Config objects or dataclasses

## 23. Anti-Patterns

- Global state everywhere
- Swallowing `Exception` without logging
- Loading entire datasets into RAM when streaming works
