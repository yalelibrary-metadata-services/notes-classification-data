# Notes Classification Project Data

**Purpose:** Classification of bibliographic notes (MARC 500 field, subfield-agnostic) based on ontological scope  
**Status:** Active  
**Last updated:** 2026-01-15

---

## Overview

Human-first classification project preparing bibliographic notes for future automated processing. Notes are classified by ontological scope: Work (w), Object (o), Administrative (a), and hybrid combinations.

**Data Pipeline:**
```
_temporary_staging/ → preprocessing → stage1_raw/ → stage2_classify/ → stage3_review/
```

---

## Directory Structure

```
.
├── config/              # Project configuration (type codes, team members)
└── data/               # Processed data (source of truth: stage1_raw/)
    ├── stage1_raw/     # Source records: 11,770 records, 50,173 notes
    ├── stage2_classify/# Classified: 3,921 records, 14,247 notes
    └── stage3_review/  # Reviewed with dual-agreement SSOT
```

*See stage-specific READMEs for detailed structures.*

---

## Statistics Summary

| Dataset | Records | Notes | Typed Notes | Empty Notes |
|---|---:|---:|---:|---:|
| raw | 11,770 | 50,173 | — | — |
| classified | 3,921 | 14,247 | 10,549 | 3,698 |
| unclassified | 7,849 | 35,926 | 0 | 35,926 |

**Type Distribution (10,549 typed notes):** o (6,432), a (2,758), w (1,195), ow (132), ao (15), aw (13), ? (4)

---

## Documentation

- [`data/stage1_raw/README.md`](data/stage1_raw/README.md) - Raw data structure and preprocessing
- [`data/stage2_classify/README.md`](data/stage2_classify/README.md) - Classification details and type distributions
- [`data/stage3_review/README.md`](data/stage3_review/README.md) - Review process and dual-agreement SSOT
- [`config/type_codes.yaml`](config/type_codes.yaml) - Classification schema
