# Raw files

**Last updated**: 2025-11-14
**Purpose**: To hold the source files yet to be classified and reviewed, and to add some organizational and structural metadata and reporting to make future work more efficient and convenient.
**Status**: Complete

## Notes

- All `bib_id` values refer to Voyager primary identifiers for the bibliographic records we're using.
- All notes are derived from MARC21 500 field.
- Each record contains one or more notes; statistics by source are documented in `raw_notes_report.csv`.
- "Person" refers to the name of the person assigned to classify records.
- Each person received their assigned file originally as XML in the form `{person_name}.xml`.
- The `_raw` suffix in current file names, `num` attributes on notes, and `all_raw` aggregate files are 'unoriginal'.
- 'Unoriginal' here denotes a small amount of pre-processing being done on the files as we received them without affecting the core content itself: for instance, across all `raws`, the order of appearance of the bib_id's have been maintained.
- The unoriginal additions:
    (1)`_raw` suffix in the file names
    (2)`num` attributes 
    (3)`path` attributes, and 
    (4)`all_raw` aggregation into a single file, 
are meant to enhance targeted and bulk QA, validation, and to support any future dynamic restructuring without affecting the integrity of the source data.
- `all_raw` arranges in alphabetic order of person_name, with bib_id order maintained.
- `XML` has a bit of a special treatment here because we are librarians, and also because it was the format that we received the pre-classified files in.
- **XML**: Root `<records>` element with `path` attribute; hierarchical structure with `<record>` elements containing `<title>` and multiple `<note num="...">` children.
- **CSV**: Flat structure with header row; one row per note containing `bib_id`, `title`, `note_num`, `note` (plus `source` column for `all_raw`).
- **JSON**: Root array of record objects; each record contains `bib_id`, `title`, and `notes` array (plus `source` field for `all_raw`).


## Data Sources

| Source | Total Records | Total Notes | 1‑Note Recs (Notes) | Multi‑Note Recs (Notes) |
|---|---:|---:|---:|---:|
| daniel_raw | 2911 | 8994 | 328 (328) | 2583 (8666) |
| martin_raw | 2752 | 16144 | 834 (834) | 1918 (15310) |
| tim_raw | 2819 | 11833 | 334 (334) | 2485 (11499) |
| will_raw | 861 | 1770 | 377 (377) | 484 (1393) |
| zoe_raw | 2427 | 11432 | 554 (554) | 1873 (10878) |
| all_raw | 11770 | 50173 | 2427 (2427) | 9343 (47746) |

## Structure examples

### Per‑person example
```xml
<?xml version='1.0' encoding='utf-8'?>
<records path="raw/XML/daniel_raw.xml">
  <record bib="17516867">
    <title>The "last best west" Canada west : homes for millions.</title>
    <note num="1">From collection: Canada Pamphlets</note>
    <note num="2">Please note: Some of the metadata for this document has been taken from the Glenbow Museum catalogue.</note>
    <note num="3">Title from publisher's website.</note>
  </record>
  ...
</records>
```

### all_raw example
```xml
<?xml version='1.0' encoding='utf-8'?>
<records path="raw/XML/all_raw.xml">
  <record bib="14520087" source="martin">
    <title>T. L. McSpadden letter, Albuquerque, New Mexico, to L. Bradford Prince, Santa Fe, New Mexico, 1912 November 11 : manuscript.</title>
    <note num="1">Title devised by cataloger.</note>
  </record>
  ...
</records>
```
