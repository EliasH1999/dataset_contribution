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

## What the key=value files represent
Each file in 'golden_keyValues/' is a **golden configuration** for one manual. The lines are expected values for a fixed set of configuration fields (our target schema). In other words, the key=values files are the ground truth used to evaluate the system

## Equivalent answers
For some fields, more than one output can be logically correct. For example:
- different address representation (e.g, Modicon vs 0-based address) if they refer to the same register
- different but equivalent formatting (e.g, hex vs decimal) depending on the manual.

## OR values
We use '|' to represent multiple valid values. The first value is the preferred/default reference, the others are acceptable alternatives. A prediction is correct if it matches any option.

## Notes on licensing
- Manuals are not redistributed in this package
- We only provide source URLs and access dates.