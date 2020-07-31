---
description: Message to indicate a fail on the operation
---

# Error

An Error Message can be sent both by clients or servers to indicate errors on a request. 

## Header

| Field | Value | Description |
| :--- | :--- | :--- |
| Message Type | 0x02 | Error |
| Message Size | varint | Remaining Message Length |

## Body

The unique available field in the Error message is the stream id which represents the ok.

| Field | Identifier | Type | Value |
| :--- | :--- | :--- | :--- |
| Stream Id | 0x01 | varint | The stream identifier that failed |
| Payload | 0x03 |  | An optional payload if the request generates any result |

## Example

