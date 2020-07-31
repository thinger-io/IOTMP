---
description: Message to indicate success on the previous request.
---

# Ok

An Ok Message can be sent both by clients or servers to indicate success on a previous request identified with its [Stream Identifier](../definitions.md#stream-identifier).

## Header

| Field | Value | Description |
| :--- | :--- | :--- |
| **Message Type** | 0x01 | Ok |
| **Message Size** | [varint](../definitions.md#varint) | Remaining Message Length |

## Body

| Field | Identifier | Type | Mandatory | Value |
| :--- | :--- | :--- | :--- | :--- |
| **Stream Id** | 0x01 | [varint](../definitions.md#varint) | Yes | [Stream identifier](../definitions.md#stream-identifier) of the source request. |
| **Response Code** | 0x02 | [varint](../definitions.md#varint) | No | Optional response code |
| **Payload** | 0x03 |  | No | Optional payload associated to the response |

## Example

### 

### 

