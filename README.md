# Notes Classification Project Data Directory
**Status:** Active
**Purpose:** This is the data directory for the notes classification project, which is about classifying bibliographic notes in MARC 500 field (subfield-agnostic) based on ontological scope
**Last updated:** 2025-12-16
**Notes:**
- 2025-12-16 update to create this README.md and to scan to verify that `classified/` is largely good to go before processing and validation work in `reviewed/` begins
- 2025-12-16 confirmation that `reviewed/` is not finalized; thus there's no `data/reviewed`

**Data directory vibes:**
- We move from **raw** -> **classified** -> **reviewed**: this is true for the `data` directory structure, and for the broad framing of the project's sequence of activities.
-- `raw` denotes unclassified
-- `classified` means person responsible has applied classification
-- `reviewed` implies at least one other member has looked at a classification applied by the original person responsible for it


## Directory Structure

- `_temporary_staging/`: holds the state of files before they make it into `data`
- `config/`: holds YAML for people and type_code information/schema
- `data/`: holds the final state usable for further work

