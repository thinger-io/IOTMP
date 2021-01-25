---
description: Message to indicate a fail on the previous request.
---

# Error

An [Error ](error.md)Message can be sent both by clients or servers to indicate an error on a previous request identified with its [Stream Identifier](../definitions.md#stream-identifier).

## Header

| Field | Value | Description |
| :--- | :--- | :--- |
| **Message Type** | 0x02 | Error |
| **Message Size** | [varint](../definitions.md#varint) | Remaining Message Length |

## Body

The unique available field in the Error message is the stream id which represents the ok.

| Name | Field | Type | Mandatory | Description |
| :--- | :--- | :--- | :--- | :--- |
| **Stream Id** | 0x01 | [varint](../definitions.md#varint) | Yes | **Stream Identifier** of the request. |
| **Parameters** | 0x02 | [any](../definitions.md#any) | No | Optional response code |
| **Payload** | 0x03 | [any](../definitions.md#any) | No | Optional payload |

## Example

