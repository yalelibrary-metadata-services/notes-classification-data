# Unclassified files

**Purpose:** Snapshot of records not yet classified  
**Status:** Active 
**Last updated:** 2026-01-09

*See root [`README.md`](../../../../README.md) for project workflow and context.*

---

## Overview

Snapshot of records from `data/raw/` that have not been classified. All notes have `type=""` (empty string). Unlike `partially_classified/` records, no note in these records has a type assigned.

**Statistics:** 7,849 records, 35,926 notes (all untyped)

---

## Structure

```
unclassified/
└── by_format/
    ├── XML/      # Per-person + all_unclassified.xml
    ├── CSV/      # Per-person + all_unclassified.csv
    └── JSON/     # Per-person + all_unclassified.json
```

**Formats:**
- **XML**: Root `<records>` with `path` attribute; `<record>` contains `<title>` and `<note type="" num="...">` children
- **CSV**: One row per note: `bib`, `title`, `note_num`, `note`, `type` (empty), `source`
- **JSON**: Array of records with `bib`, `title`, `notes` array (`text`, `note_num`, `type: ""`), `source`

---

## Relationship to Other Datasets

- **Source**: Records drawn from `data/raw/` (11,770 total records)
- **Classified**: 3,921 records moved to `data/classified/`
- **Unclassified**: 7,849 records remain here
- **Verification**: 11,770 = 3,921 + 7,849 ✓
