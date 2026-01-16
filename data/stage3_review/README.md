# Stage 3: Reviewed files

**Purpose:** Records that have undergone manual review and correction  
**Status:** Active  
**Last updated:** 2026-01-15

*See root [`README.md`](../../README.md) for project overview.*

---

## Overview

Records where classification has been manually reviewed by a second classifier. Includes normalized text (Unicode NFC) and review status fields. Provides single source of truth for notes where both classifier and reviewer agreed on type.

---

## Structure

```
stage3_review/
├── all_reviewed/      # All reviewed data (complete)
│   └── by_format/
│       ├── XML/      # Per-person + all_reviewed.xml
│       ├── CSV/      # Per-person + all_reviewed.csv
│       └── JSON/     # Per-person + all_reviewed.json
├── contentions/       # Subset: Notes where reviewers disagree (review != "y")
│   ├── daniel_reviewed_contentions.csv
│   ├── tim_reviewed_contentions.csv
│   └── zoe_reviewed_contentions.csv
└── agreements/        # Subset: Notes where reviewers agree (review = "y")
    ├── daniel_reviewed_agreements.csv
    ├── tim_reviewed_agreements.csv
    ├── zoe_reviewed_agreements.csv
    └── by_type/      # SSOT: Notes organized by type (dual-agreement only)
        ├── w.csv
        ├── o.csv
        ├── a.csv
        ├── ow.csv
        ├── aw.csv
        └── ao.csv
```

**Key Features:**
- **Normalization**: All text normalized to Unicode NFC (eliminates mojibake)
- **Review Fields**: `review` (y/n) and `reviewer` (initials) fields added
- **Field Names**: Normalized (e.g., `note_num` → `num` in CSV)

**Formats (in `all_reviewed/by_format/`):**
- **XML**: Root `<records>` with `path` attribute (e.g., `stage3_review/all_reviewed/by_format/XML/all_reviewed.xml`); `<record>` contains `bib`, `<title>`, `<note>` with `review` and `reviewer` attributes
- **CSV**: One row per note: `bib`, `title`, `num`, `type`, `note`, `review`, `reviewer` (plus `source` for `all_reviewed`)
- **JSON**: Array of records with `bib`, `title`, `notes` array (`text`, `note_num`, `type`, `review`, `reviewer`) (plus `source` for `all_reviewed`)

**Contentions:**
- Notes where `review != "y"` (disagreements/uncertainties)
- CSV files with reviewer suggestions (type and rationale)
- Supports multiple reviewers via numbered columns (reviewer_1, reviewer_2, etc.)

**Agreements:**
- Notes where `review = "y"` (dual-agreement)
- CSV files mirroring contentions structure
- **`agreements/by_type/`**: SSOT for dual-agreement notes organized by type (w, o, a, ow, aw, ao)
- Each type file contains all agreed-upon notes of that type across all reviewers

---

## Schema

**CSV**: `bib`, `title`, `num`, `type`, `note`, `review`, `reviewer` (plus `source` for aggregated files)

**JSON**: Records with `bib`, `title`, `notes` array containing `text`, `note_num`, `type`, `review`, `reviewer` (plus `source` for aggregated files)

**XML**: `<record bib="...">` with `<title>` and `<note num="..." type="..." review="..." reviewer="...">` children (plus `source` attribute for aggregated files)
