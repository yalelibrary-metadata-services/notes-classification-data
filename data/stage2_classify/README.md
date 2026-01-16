# Stage 2: Classified files

**Purpose:** Bibliographic records with notes classified by type (w/o/a and hybrids)  
**Status:** Active  
**Last updated:** 2026-01-15

*See root [`README.md`](../../README.md) for project overview.*

---

## Overview

Records with classification applied. New `type` attribute added to notes. Organized into three datasets based on type completeness.

**Statistics:** 3,921 records, 14,247 notes (10,549 typed, 3,698 empty)

---

## Structure

```
stage2_classify/
├── fully_classified/        # 3,148 records (all notes typed)
│   ├── by_format/         # XML | CSV | JSON
│   └── by_type/           # CSV by type (w/o/a/hybrids/unknown)
│
├── partially_classified/   # 773 records (mix of typed + empty)
│   ├── by_format/         # XML | CSV | JSON
│   └── by_type/           # CSV by type
│
├── unclassified/          # 7,849 records (no notes typed)
│   └── by_format/         # XML | CSV | JSON
│
└── reports/               # Validation and analysis
```

**Formats:**
- **XML**: Root `<records>` with `path` attribute (e.g., `stage2_classify/fully_classified/by_format/XML/all_classified.xml`); `<record>` contains `<title>` and `<note type="..." num="...">` children
- **CSV**: One row per note: `bib`, `title`, `note_num`, `note`, `type` (plus `source` for aggregated files)
- **JSON**: Array of records with `bib`, `title`, `notes` array (`text`, `note_num`, `type`) (plus `source` for aggregated files)
- **by_type/**: CSV files organized by classification type (w, o, a, ow, aw, ao, unknown)

---

## Statistics

### Summary

- **Total records:** 3,921 (3,148 fully_classified + 773 partially_classified)
- **Total notes:** 14,247 (6,956 fully_classified + 7,291 partially_classified)
- **Notes with types:** 10,549 (6,956 fully_classified + 3,593 partially_classified typed notes)
- **Notes with empty types:** 3,698 (all in partially_classified)

### Fully Classified

Records where all notes have non-empty type values:

| Source | Total Records | Total Notes | w | o | a | aw | ow | ao | Unknown (?) |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| daniel_classified | 500 | 1,011 | 58 | 397 | 551 | 3 | 0 | 1 | 1 |
| martin_classified | 393 | 598 | 116 | 42 | 408 | 2 | 29 | 0 | 1 |
| tim_classified | 21 | 59 | 18 | 30 | 5 | 2 | 3 | 1 | 0 |
| will_classified | 500 | 870 | 100 | 713 | 48 | 1 | 2 | 6 | 0 |
| zoe_classified | 1,734 | 4,418 | 475 | 3,258 | 578 | 7 | 93 | 7 | 0 |
| **Total** | **3,148** | **6,956** | **767** | **4,440** | **1,590** | **15** | **127** | **15** | **2** |

*Type codes: w (work), o (object), a (administrative). Hybrids: aw, ow, ao. See `config/type_codes.yaml`.*

### Partially Classified

Records with both empty and non-empty type notes (binary split: entire record moved if any note has empty type):

| Source | Total Records | Total Notes | Empty Type Notes | w | o | a | aw | ow | ao | Unknown (?) |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| combined | 773 | 7,291 | 3,698 | 428 | 1,992 | 1,168 | 1 | 2 | 0 | 2 |
| typed_only | 773 | 3,593 | 0 | 428 | 1,992 | 1,168 | 1 | 2 | 0 | 2 |
| empties_only | 773 | 3,698 | 3,698 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| martin_only | 158 | 431 | 251 | 14 | 3 | 158 | 1 | 2 | 0 | 2 |
| zoe_only | 615 | 6,860 | 3,447 | 414 | 1,989 | 1,010 | 0 | 0 | 0 | 0 |
| **Total** | **773** | **7,291** | **3,698** | **428** | **1,992** | **1,168** | **1** | **2** | **0** | **2** |

---

## Dataset Splits

- **fully_classified/**: All notes have type values (3,148 records)
- **partially_classified/**: Mix of typed and empty type notes (773 records). Binary split: entire record moved if any note has empty type.
- **unclassified/**: Snapshot of records not yet classified (7,849 records)

---

## Reports

- `reports/summary.md` - Current statistics summary
