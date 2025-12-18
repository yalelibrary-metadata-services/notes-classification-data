# Classified files

* **Purpose**: Bibliographic records with notes classified by type (w/o/a and hybrids), organized by person
* **Last updated**: 2025-12-17
* **Status**: Complete
* **Notes:**
  - New attribute, `type`, added to indicate a given note's classification; this attribute is not in `raw/` files.
  - The **XML** has root `<records>` element with `path` attribute; hierarchical structure with `<record>` elements containing `<title>` and multiple `<note type="..." num="...">` children.
  - **CSV**: Flat structure with header row; one row per note containing `bib_id`, `title`, `note_num`, `note`, `type` (plus `source` column for aggregated files).
  - **JSON**: Root array of record objects; each record contains `bib_id`, `title`, and `notes` array with `text`, `note_num`, `type` (plus `source` field for aggregated files).
  - **fully_classified** files contain only records where all notes have non-empty values for @type.
  - **partially_classified** files contain records with at least one non-empty and one empty type note.

---
## Data Sources

### Summary

- **Total records:** 3,921 (3,148 fully_classified + 773 partially_classified)
- **Total notes:** 14,247 (6,956 fully_classified + 7,291 partially_classified)
- **Notes with types:** 10,549 (6,956 fully_classified + 3,593 partially_classified typed notes)
- **Notes with empty types:** 3,698 (all in partially_classified)

### Fully Classified

Records where all notes have non-empty type values are located in `classified/fully_classified/by_format/`:

| Source | Total Records | Total Notes | w | o | a | aw | ow | ao | Unknown (?) |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| daniel_classified | 500 | 1,011 | 58 | 397 | 551 | 3 | 0 | 1 | 1 |
| martin_classified | 393 | 598 | 116 | 42 | 408 | 2 | 29 | 0 | 1 |
| tim_classified | 21 | 59 | 18 | 30 | 5 | 2 | 3 | 1 | 0 |
| will_classified | 500 | 870 | 100 | 713 | 48 | 1 | 2 | 6 | 0 |
| zoe_classified | 1,734 | 4,418 | 475 | 3,258 | 578 | 7 | 93 | 7 | 0 |
| **Total** | **3,148** | **6,956** | **767** | **4,440** | **1,590** | **15** | **127** | **15** | **2** |

*Type Distribution: w (work), o (object), a (administrative). Hybrids: aw (administrative-work), ow (object-work), ao (administrative-object).*

### Partially Classified

Records with both empty and non-empty type notes (binary split) are located in `classified/partially_classified/by_format/`:

| Source | Total Records | Total Notes | Empty Type Notes | w | o | a | aw | ow | ao | Unknown (?) |
|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| combined | 773 | 7291 | 3698 | 428 | 1992 | 1168 | 1 | 2 | 0 | 2 |
| typed_only | 773 | 3593 | 0 | 428 | 1992 | 1168 | 1 | 2 | 0 | 2 |
| empties_only | 773 | 3698 | 3698 | 0 | 0 | 0 | 0 | 0 | 0 | 0 |
| martin_only | 158 | 431 | 251 | 14 | 3 | 158 | 1 | 2 | 0 | 2 |
| zoe_only | 615 | 6860 | 3447 | 414 | 1989 | 1010 | 0 | 0 | 0 | 0 |
| **Total** | **773** | **7,291** | **3,698** | **428** | **1,992** | **1,168** | **1** | **2** | **0** | **2** |

---
## Structure Examples

### fully_classified file example
```xml
<?xml version='1.0' encoding='utf-8'?>
<records path="classified/fully_classified/by_format/XML/daniel_classified.xml">
  <record bib="17516867">
    <title>The "last best west" Canada west : homes for millions.</title>
    <note type="w" num="1">From collection: Canada Pamphlets</note>
    <note type="a" num="2">Please note: Some of the metadata for this document has been taken from the Glenbow Museum catalogue.</note>
    <note type="a" num="3">Title from publisher's website.</note>
  </record>
  ...
</records>
```

### partially_classified file example
```xml
<?xml version='1.0' encoding='utf-8'?>
<records path="classified/partially_classified/by_format/XML/combined.xml">
  <record bib="14526311" source="martin">
    <title>Example title</title>
    <note type="w" num="1">Classified note</note>
    <note type="" num="2">Unclassified note</note>
    <note type="a" num="3">Classified note</note>
  </record>
  ...
</records>
```
---
## Validation Reports

- `reports/reports_2025-12-17/` - Latest validation reports including meta-validation and by-type accounting
- `reports/reports_2025-11-14/` - Initial validation and processing reports covering metadata accuracy, statistics, type presence analysis, empty type handling, and final reorganization

*Note: File and folder names referenced in past reports may have changed due to reorganization.*