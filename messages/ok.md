---
description: Message to indicate success on the operation
---

# Ok

An Ok Message can be sent both by clients or servers to indicate success on a request. 

## Header

| Field | Value | Description |
| :--- | :--- | :--- |
| Message Type | 0x01 | Ok |
| Message Size | varint | Remaining Message Length |

## Body

The unique available field in the Ok message is the stream id which represents the ok.

| Field | Identifier | Type | Value |
| :--- | :--- | :--- | :--- |
| Stream Id | 0x01 | varint | The stream identifier that succeed |

## Example

### 

### 

