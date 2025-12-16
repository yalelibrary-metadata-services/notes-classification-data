# Classified files (temporary_staging/classified)

**Last updated**: 2025-11-14
**Purpose**: Bibliographic records with notes classified by type (w/o/a and hybrids), organized by person.
**Status**: Complete - Main files validated with 100% type attribute coverage and zero empty types.

## Notes

- All `bib_id` values refer to Voyager primary identifiers for bibliographic records.
- All notes are derived from MARC21 500 field.
- Each note has been classified with a `type` attribute indicating the note's classification.
- "Person" refers to the name of the person assigned to classify records.
- **XML**: Root `<records>` element with `path` attribute; hierarchical structure with `<record>` elements containing `<title>` and multiple `<note type="..." num="...">` children.
- Classification scheme uses: **w** (work), **o** (object), **a** (admin), and hybrids (**aw**, **ow**, **ao**), plus **?** for uncertain cases.
- Main classified files contain only records where all notes have non-empty type values.
- Records with at least one empty type value (`type=""`) are isolated in `XML/empty_types/` subdirectory.

## Data Sources

| Source | Total Records | Total Notes | Type Distribution (w/o/a) | Hybrids (aw/ow/ao) | Unknown (?) |
|---|---:|---:|---|---|---:|
| daniel_classified | 500 | 1,011 | 58 / 397 / 551 | 3 / 0 / 1 | 1 |
| martin_classified | 393 | 778 | 130 / 45 / 566 | 3 / 31 / 0 | 3 |
| tim_classified | 21 | 59 | 18 / 30 / 5 | 2 / 3 / 1 | 0 |
| will_classified | 500 | 870 | 100 / 713 / 48 | 1 / 2 / 6 | 0 |
| zoe_classified | 1,734 | 7,831 | 889 / 5,247 / 1,588 | 7 / 93 / 7 | 0 |
| **Total (main files)** | **3,148** | **10,549** | **1,195 / 6,432 / 2,758** | **16 / 129 / 15** | **4** |

### Empty Types Subdirectory

Records with at least one empty type value are isolated in `XML/empty_types/`:

| Source | Total Records | Total Notes | Empty Type Notes |
|---|---:|---:|---:|
| martin_with_empty_types | 158 | 251 | 251 |
| zoe_with_empty_types | 615 | 3,447 | 3,447 |
| **Total (empty_types)** | **773** | **3,698** | **3,698** |

**Note:** Original martin and zoe files contained 551 and 2,349 records respectively. Main classified files now contain only records with complete classifications.

## Classification Status

### Main Files (XML/)
- ✓ **100% type attribute coverage** - All 10,549 notes have `type` attribute present
- ✓ **Zero empty types** - All type values are non-empty (w/o/a/hybrids/?)
- ✓ **Path attributes updated** - All files have correct `path` attribute on root `<records>` element

### Empty Types Subdirectory (XML/empty_types/)
- Contains 773 records with partial classifications (at least one note has `type=""`)
- Awaiting further classification work
- Binary split: entire record moved if any note has empty type

## Structure Examples

### Main classified file example
```xml
<?xml version='1.0' encoding='utf-8'?>
<records path="classified/XML/daniel_classified.xml">
  <record bib="17516867">
    <title>The "last best west" Canada west : homes for millions.</title>
    <note type="w" num="1">From collection: Canada Pamphlets</note>
    <note type="a" num="2">Please note: Some of the metadata for this document has been taken from the Glenbow Museum catalogue.</note>
    <note type="a" num="3">Title from publisher's website.</note>
  </record>
  ...
</records>
```

### Empty types file example
```xml
<?xml version='1.0' encoding='utf-8'?>
<records path="classified/XML/empty_types/martin_with_empty_types.xml">
  <record bib="14526311">
    <title>Example title</title>
    <note type="w" num="1">Classified note</note>
    <note type="" num="2">Unclassified note</note>
    <note type="a" num="3">Classified note</note>
  </record>
  ...
</records>
```

## Validation Reports

Detailed validation reports are available in `reports/`:
- `p2t2.1_stats_20251114_084732.md` - Initial statistics and type distribution
- `p3t3.1_type_presence_20251114_085004.md` - Type attribute presence verification
- `p3t3.2_empty_types_20251114_085047.md` - Empty type values analysis
- `p4t4.1_split_20251114_085819.md` - Binary split files report
- `p4t4.1_final_reorg_20251114_091800.md` - Final reorganization and verification
