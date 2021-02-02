---
description: Message used to represent information transmitted over a stream.
---

# Stream Data

## Message

### Header

| Field | Value | Description |
| :--- | :--- | :--- |
| **Message Type** | 0x0A | Stream Data |
| **Message Size** | [varint](../../definitions.md#varint) | Remaining Message Length |

### Body

| Field | Identifier | Type | Mandatory | Value |
| :--- | :--- | :--- | :--- | :--- |
| **Stream Id** | 0x01 | [varint](../../definitions.md#varint) | Yes | Stream identifier. |
| **Parameters** | 0x02 | [any](../../definitions.md#any) | No | User-defined parameters associated to the information that can be used for signaling the payload, provide a context, etc. |
| **Payload** | 0x03 | [any](../../definitions.md#any) | No | Current stream payload. |
| **Scope** | 0x04 | [varint](../../definitions.md#varint) | No |  |

## Thinger.io

In thinger.io, clients streaming resources establish the following parameters to help the server identifying the source of information while sending data.

### Parameters

| Name | Value | Description |
| :--- | :--- | :--- |
| **Resource Input** | 0x01 | Stream data represents the input of the stream resource. |
| **Resource Output** | 0x02 | Stream data represents the output of the stream resource. |



