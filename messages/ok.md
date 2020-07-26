---
description: Message to indicate success on the operation
---

# Ok

## Header

| Field | Value | Description |
| :--- | :--- | :--- |
| Message Type | 0x01 |  |
| Message Size | 0x00 |  |

## Body

The unique available field in the Ok message is the stream id which represents the ok.

| Field | Type | Description |
| :--- | :--- | :--- |
| Stream Id | varint |  |

## Example

### Ok Without Stream Id

```text
0x01 0x00
```

### OK With Stream Id

```text
0x01 0x00 00000000 0x60
```

### 

