# Python Field Manual

A practical, opinionated reference for:

- Python automation and integration
- Text processing and data cleaning
- Databases and ETL (SQLite, Postgres, Oracle)
- Quality practices (logging, testing, typing, architecture)
- Tutoring Python to kids, teens, and adults
- A ready-to-use script cookbook

This manual is designed for:

- Automation / integration engineers
- Data / ETL folks
- SRE / DevOps / platform engineers
- Tutors and mentors who teach Python
- Anyone who wants real-world, “pays-rent” Python patterns

---

## Structure

The manual is split into seven main parts:

1. **Part 0 – Setup & Muscle Memory**
   Environment, venv, script skeletons, project layout.

2. **Part 1 – Core Language**
   Names and objects, control flow, collections, functions, generators.

3. **Part 2 – Text, Files, and Data Cleaning**
   Strings, regex, files, encodings, CSV/JSON/YAML, cleanup pipelines.

4. **Part 3 – System Automation & Integration**
   `os`, `pathlib`, `shutil`, `subprocess`, HTTP APIs, retries, schedulers.

5. **Part 4 – Databases & ETL**
   DB-API patterns, SQLite, Postgres, Oracle, ETL pipeline skeletons.

6. **Part 5 – Quality Layer**
   Logging, testing, type hints, architecture patterns, anti-patterns.

7. **Part 6 – Tutoring Toolkit**
   Teaching strategies, debugging lessons, project ideas.

8. **Part 7 – Script Cookbook**
   A library of ready-to-adapt scripts (log rotator, CSV cleaner, API→DB sync, SQL report, directory scanner, URL checker, JSON→Oracle loader).

---

## How to Read / Use

- Use the **GitBook site** (once connected) for navigation, search, and nice formatting.
- Browse the **`chapters/` directory** directly if you prefer working in Markdown.
- Copy scripts from **Part 7** into your own `scripts/` folder and adapt them to real work.

---

## Local Preview

You can read the manual locally with any Markdown viewer, or open it in VS Code:

```bash
git clone <your-repo-url>
cd python-field-manual
code .
