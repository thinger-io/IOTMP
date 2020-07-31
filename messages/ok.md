---
description: Message to indicate success on the operation
---

# Ok

An Ok Message can be sent both by clients or servers to indicate success on a request. 

## Header

| Field | Value | Description |
| :--- | :--- | :--- |
| **Message Type** | 0x01 | Ok |
| **Message Size** | varint | Remaining Message Length |

## Body

The unique available field in the Ok message is the stream id which represents the ok.

| Field | Identifier | Type | Mandatory | Value |
| :--- | :--- | :--- | :--- | :--- |
| **Stream Id** | 0x01 | varint | Yes | [Stream identifier](../definitions.md#stream-identifier) of the source request. |
| **Response Code** | 0x02 | varint | No | Optional response code |
| **Payload** | 0x03 |  | No | Optional payload if the request generates any result |

## Example

### 

### 

