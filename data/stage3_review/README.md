# Stage 3: Reviewed files

**Purpose:** Records that have undergone manual review and correction  
**Status:** Active  
**Last updated:** 2026-01-15

*See root [`README.md`](../../README.md) for project workflow and context.*

---

## Overview

Records where classification and metadata have been manually reviewed and verified. This dataset resolves mojibake issues found in earlier stages and normalizes field names.

**Statistics:** (See validation summary)

---

## Structure

```
stage3_review/
├── by_format/
│   ├── XML/      # Per-person XML
│   ├── CSV/      # Per-person CSV
│   └── JSON/     # Per-person JSON
└── contentions/  # Notes where reviewers disagree with classification
    ├── daniel_reviewed_contentions.csv
    ├── tim_reviewed_contentions.csv
    └── zoe_reviewed_contentions.csv
```

**Formats:**
- **XML**: Root `<records>` with `path` attribute; `<record>` contains `bib` attribute, `<title>`, and `<note>` children.
- **CSV**: One row per note. Header: `bib`, `title`, `num`, `type`, `note`, `review`, `reviewer`.
- **JSON**: Array of records with `bib`, `title`, and `notes` array (`text`, `note_num`, `type`, `review`, `reviewer`).

**Key Differences from Other Datasets:**
- **Normalization**: All text is normalized to Unicode NFC to eliminate mojibake.
- **Review Fields**: Includes `review` (y/n status) and `reviewer` (initials) fields.

**Contentions:**
- Notes where reviewers disagree with the original classification (`review != "y"`)
- Stored in `contentions/` folder as CSV files
- Each file contains reviewer suggestions (type and rationale) for resolving disagreements
- Supports multiple reviewers adding input using numbered columns (reviewer_1, reviewer_2, etc.)

---

## Schema Details

### CSV
`bib`, `title`, `num`, `type`, `note`, `review`, `reviewer`

### JSON
```json
{
  "bib": "123456",
  "title": "Example Title",
  "notes": [
    {
      "text": "Note text",
      "note_num": 1,
      "type": "w",
      "review": "y",
      "reviewer": "abc"
    }
  ]
}
```

### XML
```xml
<record bib="123456">
  <title>Example Title</title>
  <note num="1" type="w" review="y" reviewer="abc">Note text</note>
</record>
```
