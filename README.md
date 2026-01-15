# Notes Classification Project Data

**Purpose:** Classification of bibliographic notes (MARC 500 field, subfield-agnostic) based on ontological scope  
**Status:** Active  
**Last updated:** 2026-01-09

---

## Directory Structure

```
.
├── _temporary_staging/          # Landing point for received files
│   └── reviewed/               # Deferred review work
│
├── config/                      # Project configuration
│   ├── type_codes.yaml         # Classification schema (w/o/a + hybrids)
│   └── people.yaml             # Team members and roles
│
└── data/                        # Processed data (source of truth: stage1_raw/)
    │
    ├── stage1_raw/              # Source records: 11,770 records, 50,173 notes
    │   └── by_format/          # XML | CSV | JSON
    │
    ├── stage2_classify/        # Classified records: 3,921 records, 14,247 notes
    │   ├── fully_classified/   # 3,148 records (all notes typed)
    │   │   ├── by_format/      # XML | CSV | JSON
    │   │   └── by_type/        # CSV (w/o/a/hybrids/unknown)
    │   │
    │   ├── partially_classified/  # 773 records (mix of typed + empty)
    │   │   ├── by_format/      # XML | CSV | JSON
    │   │   └── by_type/        # CSV (w/o/a/hybrids/unknown)
    │   │
    │   ├── unclassified/       # Snapshot: 7,849 records, 35,926 notes
    │   │   └── by_format/      # XML | CSV | JSON
    │   │
    │   └── reports/             # Validation and analysis
    │       ├── reports_2025-12-17/
    │       └── reports_2025-11-14/
    │
    └── stage3_review/           # Reviewed records with normalized classifications
        ├── by_format/          # XML | CSV | JSON
        └── contentions/         # Notes where reviewers disagree with classification
```

---

## Workflow

**Data Pipeline:**
```
_temporary_staging/ → preprocessing → data/stage1_raw/ → data/stage2_classify/ → data/stage3_review/
```

- **`_temporary_staging/`**: Files land here before preprocessing into `data/`
- **`data/stage1_raw/`**: Source bibliographic records (11,770 records)
- **`data/stage2_classify/`**: Records with classification applied (3,921 records)
  - **fully_classified**: All notes have type values (3,148 records)
  - **partially_classified**: Mix of typed and empty type notes (773 records)
  - **unclassified**: Snapshot of records not yet classified (7,849 records)
- **`data/stage3_review/`**: Second classifier review with normalized classification files
  - **contentions**: Notes where reviewers disagree with original classification

**Partially Classified:** Records containing both typed and empty type notes. Binary split: entire record moved if any note has empty type. Unlike `unclassified/`, these records have at least one typed note.

---

## Statistics Summary

| Dataset | Records | Notes | Typed Notes | Empty Notes |
|---|---:|---:|---:|---:|
| raw | 11,770 | 50,173 | — | — |
| classified | 3,921 | 14,247 | 10,549 | 3,698 |
| unclassified | 7,849 | 35,926 | 0 | 35,926 |

*Verification:* 
- **11,770** = 3,921 + 7,849
- **50,173** = 14,247 + 35,926

### Type Distribution (10,549 Classified Notes)

| Code | Count | Definition |
|---|---|:---|
| w | 1,195 | Work |
| o | 6,432 | Object |
| a | 2,758 | Administrative |
| ow | 132 | Object + Work |
| aw | 13 | Administrative + Work |
| ao | 15 | Administrative + Object |
| ? | 4 | Unknown |
| (empty) | 3,698 | Unclassified |

*Schema details: `config/type_codes.yaml`*

---

## Formats & Access

- **XML/CSV/JSON**: Available in `by_format/` subdirectories
- **Type-specific CSV**: Available in `by_type/` directories (CSV only for ease of use)
- **Reports**: `data/classified/reports/` (may reference older directory structures)

---

## Documentation

- `data/stage1_raw/README.md` - Raw data structure
- `data/stage2_classify/README.md` - Classified details and type distributions  
- `data/stage2_classify/unclassified/by_format/README.md` - Unclassified snapshot
- `data/stage3_review/README.md` - Review process and contentions
- `config/type_codes.yaml` - Classification schema
