# Validation Report 2025-12-17

**Discrepancies:** Part 4.2 Final Report and README have incorrect note counts for martin and zoe files.

**Findings:** 
    - martin_classified.xml has 598 notes (not 778), 
    - martin_with_empty_types.xml has 431 total notes (not 251), 
    - zoe_classified.xml has 4418 notes (not 7831), 
    - zoe_with_empty_types.xml has 6860 total notes (not 3447)
    
Empty-type note counts (251, 3447) are correct; the reports only counted empty-type notes for empty_types files, not total notes. All arithmetic totals remain correct.

