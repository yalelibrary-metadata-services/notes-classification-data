# Stage 2: Classified files

**Purpose:** Bibliographic records with notes classified by type (w/o/a and hybrids)  
**Status:** Active  
**Last updated:** 2026-01-15

*See root [`README.md`](../../README.md) for project workflow and context.*

---

## Overview

Records with classification applied. New `type` attribute added to notes (not present in `stage1_raw/` files). Organized into `fully_classified/` (all notes typed), `partially_classified/` (mix of typed and empty), and `unclassified/` (no notes typed).

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
- **XML**: Root `<records>` with `path` attribute; `<record>` contains `<title>` and `<note type="..." num="...">` children
- **CSV**: One row per note: `bib`, `title`, `note_num`, `note`, `type` (plus `source` for aggregated files)
- **JSON**: Array of records with `bib`, `title`, `notes` array (`text`, `note_num`, `type`) (plus `source` for aggregated files)
- **by_type/**: CSV files organized by classification type (CSV only for ease of use)

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

## Structure Examples

### fully_classified
```xml
<?xml version='1.0' encoding='utf-8'?>
<records path="stage2_classify/fully_classified/by_format/XML/daniel_classified.xml">
  <record bib="17516867">
    <title>The "last best west" Canada west : homes for millions.</title>
    <note type="w" num="1">From collection: Canada Pamphlets</note>
    <note type="a" num="2">Please note: Some of the metadata...</note>
  </record>
</records>
```

### partially_classified
```xml
<?xml version='1.0' encoding='utf-8'?>
<records path="stage2_classify/partially_classified/by_format/XML/combined.xml">
  <record bib="14526311" source="martin">
    <title>Example title</title>
    <note type="w" num="1">Classified note</note>
    <note type="" num="2">Unclassified note</note>
    <note type="a" num="3">Classified note</note>
  </record>
</records>
```

---

## Validation Reports

- `reports/reports_2025-12-17/` - Latest validation reports including meta-validation and by-type accounting
- `reports/reports_2025-11-14/` - Initial validation and processing reports

*Note: File and folder names referenced in past reports may have changed due to reorganization.*
