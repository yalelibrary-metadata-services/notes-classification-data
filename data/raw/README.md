# Raw files

**Purpose:** Source bibliographic records before classification  
**Status:** Complete  
**Last updated:** 2025-11-14

*See root [`README.md`](../../README.md) for project workflow and context.*

---

## Overview

Source records from MARC21 500 fields, preprocessed for organizational and structural metadata. Files land in `_temporary_staging/` before preprocessing into `data/raw/`.

**Statistics:** 11,770 records, 50,173 notes

---

## Structure

```
raw/
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

| Source | Total Records | Total Notes | 1‑Note Recs (Notes) | Multi‑Note Recs (Notes) |
|---|---:|---:|---:|---:|
| daniel_raw | 2,911 | 8,994 | 328 (328) | 2,583 (8,666) |
| martin_raw | 2,752 | 16,144 | 834 (834) | 1,918 (15,310) |
| tim_raw | 2,819 | 11,833 | 334 (334) | 2,485 (11,499) |
| will_raw | 861 | 1,770 | 377 (377) | 484 (1,393) |
| zoe_raw | 2,427 | 11,432 | 554 (554) | 1,873 (10,878) |
| **all_raw** | **11,770** | **50,173** | **2,427 (2,427)** | **9,343 (47,746)** |

---

## Preprocessing Notes

Files received as `{person_name}.xml` were preprocessed with minimal additions:
- `_raw` suffix in filenames
- `num` attributes on notes
- `path` attributes on root elements
- `all_raw` aggregation (alphabetical by person, bib_id order maintained)

These additions support QA, validation, and future restructuring without affecting source data integrity. All `bib_id` values refer to Voyager primary identifiers.

---

## Structure Examples

### Per-person file
```xml
<?xml version='1.0' encoding='utf-8'?>
<records path="raw/by_format/XML/daniel_raw.xml">
  <record bib="17516867">
    <title>The "last best west" Canada west : homes for millions.</title>
    <note num="1">From collection: Canada Pamphlets</note>
    <note num="2">Please note: Some of the metadata...</note>
  </record>
</records>
```

### Aggregated file
```xml
<?xml version='1.0' encoding='utf-8'?>
<records path="raw/by_format/XML/all_raw.xml">
  <record bib="14520087" source="martin">
    <title>T. L. McSpadden letter...</title>
    <note num="1">Title devised by cataloger.</note>
  </record>
</records>
```

---

## Reports

- `reports/raw_notes_report.csv` - Statistics by source
