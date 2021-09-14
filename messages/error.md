---
description: Message to indicate an error on the previous request.
---

# Error

An [Error ](error.md)Message can be sent both by clients or servers to indicate an error on a previous request identified with its [Stream Identifier](../definitions.md#stream-identifier).

## Header

| Field | Value | Description |
| :--- | :--- | :--- |
| **Message Type** | 0x02 | Error |
| **Message Size** | [varint](../definitions.md#varint) | Remaining Message Length |

## Body

| Name | Field | Type | Mandatory | Description |
| :--- | :--- | :--- | :--- | :--- |
| **Stream Id** | 0x01 | [varint](../definitions.md#varint) | Yes | [Stream identifier](../definitions.md#stream-identifier) of the source request. |
| **Parameters** | 0x02 | [any](../definitions.md#any) | No | Optional parameters associated to the response, like a response code, payload description, etc. |
| **Payload** | 0x03 | [any](../definitions.md#any) | No | Optional payload associated to the response |

## Example

