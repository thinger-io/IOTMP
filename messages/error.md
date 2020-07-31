---
description: Message to indicate a fail on the operation
---

# Error

An Error Message can be sent both by clients or servers to indicate errors on a request. 

## Header

| Field | Value | Description |
| :--- | :--- | :--- |
| **Message Type** | 0x02 | Error |
| **Message Size** | varint | Remaining Message Length |

## Body

The unique available field in the Error message is the stream id which represents the ok.

| Field | Identifier | Type | Mandatory | Value |
| :--- | :--- | :--- | :--- | :--- |
| **Stream Id** | 0x01 | varint | Yes | **Stream Identifier** of the request. |
| **Response Code** | 0x02 | varint | No | Optional response code |
| **Payload** | 0x03 |  |  | Optional payload |

## Example

