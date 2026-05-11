# Dataset for "Automated Configuration Generation Based on Device Manuals"

This package contains the evaluation dataset used in our thesis.

## Contents
- 'manual_inventory.csv'
    - Columns 'manual_id', 'golden_file', 'source_url', 'access_date'
- 'golden_keyValues/'
    - One file per manual
    - Each file contains key=value lines in our fixed schema.

## How to use
1. Pick a manual from 'manual_inventory.csv'.
2. Download the manual using the 'source_url'.
3. Compare model output against the corresponding golden_keyValues file listed in the golden_keyValues folder.

## Golden format
- Files contain one 'key=value' per line.
- Keys follow our Anybus JSON configuration schema.
- Missing values are recorded as 'not found'.

## Notes on licensing
- Manuals are not redistributed in this package
- We only provide source URLs and access dates.