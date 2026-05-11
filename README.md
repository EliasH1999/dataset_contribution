# Dataset for "Automated Configuration Generation Based on Device Manuals"

This package contains the evaluation dataset used in our thesis.

## Contents
- `manual_inventory.csv`
    - Columns `manual_id`, `golden_file`, `source_url`, `access_date`
- `golden_keyValues/`
    - One file per manual
    - Each file contains key=value lines in our fixed schema.

## How to use
1. Pick a manual from `manual_inventory.csv`.
2. Download the manual using the `source_url`.
3. Compare model output against the corresponding golden_keyValues file listed in the golden_keyValues folder.

## Golden format
- Files contain one `key=value` per line.
- Keys follow our Anybus JSON configuration schema.
- Missing values are recorded as `not found`.

## Key meanings
The golden files mirror the Anybus Communicator JSON structure. These keys mean the following.

### Serial / subnetwork settings
- `subnetwork.properties.physicalStandard` = Physical standard
- `subnetwork.properties.baudRate` = Modbus RTU baud rate
- `subnetwork.properties.parity` = Parity bits
- `subnetwork.properties.stopBits` = Stop bits
- `subnetwork.properties.dataBits` = Data bits

### Node settings (the Modbus device)
- `subnetwork.nodes[0].properties.nodeAddress` = Modbus Unit ID / slave address
- `subnetwork.nodes[0].properties.name` = human readable node name
- `subnetwork.nodes[0].properties.modbusAddressingMode` = addressing mode used by Anybus

### Transaction settings
- `subnetwork.nodes[0].transactions[0].properties.name` = transaction name

### Frames (request/response)
- `subnetwork.nodes[0].transactions[0].frames[0]` = request frame (the Modbus request)
- `subnetwork.nodes[0].transactions[0].frames[1]` = response frame (the Modbus response)

### Request fields (frames[0])
- `subnetwork.nodes[0].transactions[0].frames[0].frameObjects[1].properties.data` = Modbus function code
- `subnetwork.nodes[0].transactions[0].frames[0].frameObjects[2].properties.data` = Start address
- `subnetwork.nodes[0].transactions[0].frames[0].frameObjects[3].properties.data` = Quantity (number of registers/coils)

### Response fields (frames[1])
- `subnetwork.nodes[0].transactions[0].frames[1].frameObjects[1].properties.data` = Modbus function code
- `subnetwork.nodes[0].transactions[0].frames[1].frameObjects[2].properties.data` = Byte count (number of data bytes in the response, for registers this is typically quantity * 2)
- `subnetwork.nodes[0].transactions[0].frames[1].frameObjects[3].properties.dataLength` = Response payload length in bytes

## What the key=value files represent
Each file in `golden_keyValues/` is a **golden configuration** for one manual. The lines are expected values for a fixed set of configuration fields (our target schema). In other words, the key=values files are the ground truth used to evaluate the system

## Equivalent answers
For some fields, more than one output can be logically correct. For example:
- different address representation (e.g, Modicon vs 0-based address) if they refer to the same register
- different but equivalent formatting (e.g, hex vs decimal) depending on the manual.

## OR values
We use `|` to represent multiple valid values. The first value is the preferred/default reference, the others are acceptable alternatives. A prediction is correct if it matches any option.

## Notes on licensing
- Manuals are not redistributed in this package
- We only provide source URLs and access dates.