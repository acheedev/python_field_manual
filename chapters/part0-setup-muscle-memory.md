[Home](../README.md) · [Next → Part 1 – Core Language](part1-core-language.md)
---

# Part 0 – Setup & Muscle Memory

## 0.1 Python Toolchain for Practical Automation

You are writing **scripts**, not academic exercises. You need a setup that is reliable, minimal, and portable across Linux, macOS, and Windows (including WSL).

### Key principles

- Use **Python 3** only.
- Use **virtual environments** (`venv`) per project.
- Do **not** install packages into system Python.
- Use **VS Code** with the Python extension, Pylance, and Black.

### Create a virtual environment

```bash
python3 -m venv .venv
source .venv/bin/activate   # Windows: .venv\Scripts\activate
pip install --upgrade pip setuptools wheel
```

### Simple project layout

```text
project/
  ├── scripts/
  │     └── myscript.py
  ├── lib/
  │     └── helpers.py
  ├── .venv/
  ├── requirements.txt
  └── README.md
```

## 0.2 Universal Script Skeleton

Use this strict, reusable pattern in every automation script. It gives you:

- CLI flags
- logging with verbosity
- `--dry-run` support
- a clear `main()` entrypoint

```python
#!/usr/bin/env python3
"""Describe what the script does."""

import argparse
import logging
import sys

LOG = logging.getLogger("script")

def parse_args():
    p = argparse.ArgumentParser(description="Describe your script")
    p.add_argument("--dry-run", action="store_true")
    p.add_argument("--verbose", "-v", action="count", default=0)
    p.add_argument("input", nargs="?")
    return p.parse_args()

def setup_logging(verbosity: int):
    level = logging.WARNING
    if verbosity == 1:
        level = logging.INFO
    elif verbosity >= 2:
        level = logging.DEBUG

    logging.basicConfig(
        level=level,
        format="%(asctime)s [%(levelname)s] %(message)s",
    )

def main():
    args = parse_args()
    setup_logging(args.verbose)
    LOG.info("Start")
    if args.dry_run:
        LOG.warning("DRY RUN mode")
    LOG.debug("Input: %s", args.input)
    # main logic here
    return 0

if __name__ == "__main__":
    sys.exit(main())
```

## 0.3 Environment Setup Workflow

- Windows + WSL notes
- Linux/macOS quick steps
- `pip install -r requirements.txt`
- How to freeze dependencies with `pip freeze > requirements.txt`
