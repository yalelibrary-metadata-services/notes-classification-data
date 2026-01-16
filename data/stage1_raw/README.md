# Stage 1: Raw files

**Purpose:** Source bibliographic records before classification  
**Status:** Complete  
**Last updated:** 2026-01-15

*See root [`README.md`](../../README.md) for project overview.*

---

## Overview

Source records from MARC21 500 fields, preprocessed for organizational and structural metadata. Files land in `_temporary_staging/` before preprocessing into `data/stage1_raw/`.

**Statistics:** 11,770 records, 50,173 notes

---

## Structure

```
stage1_raw/
└── by_format/
    ├── XML/      # Per-person + all_raw.xml
    ├── CSV/      # Per-person + all_raw.csv
    └── JSON/     # Per-person + all_raw.json
```

**Formats:**
- **XML**: Root `<records>` with `path` attribute; `<record>` contains `<title>` and `<note num="...">` children
- **CSV**: One row per note: `bib`, `title`, `note_num`, `note` (plus `source` for `all_raw`)
- **JSON**: Array of records with `bib`, `title`, `notes` array (plus `source` for `all_raw`)

---

## Data Sources

| Source | Records | Notes | 1‑Note Recs | Multi‑Note Recs |
|---|---:|---:|---:|---:|
| daniel_raw | 2,911 | 8,994 | 328 | 2,583 |
| martin_raw | 2,752 | 16,144 | 834 | 1,918 |
| tim_raw | 2,819 | 11,833 | 334 | 2,485 |
| will_raw | 861 | 1,770 | 377 | 484 |
| zoe_raw | 2,427 | 11,432 | 554 | 1,873 |
| **all_raw** | **11,770** | **50,173** | **2,427** | **9,343** |

---

## Preprocessing

Files received as `{person_name}.xml` were preprocessed with minimal additions:
- `_raw` suffix in filenames
- `num` attributes on notes
- `path` attributes on root elements (e.g., `stage1_raw/by_format/XML/all_raw.xml`)
- `all_raw` aggregation (alphabetical by person, bib_id order maintained)

All `bib_id` values refer to Voyager primary identifiers.

---

## Reports

- `reports/raw_notes_report.csv` - Statistics by source
