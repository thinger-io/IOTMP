---
description: Message used to represent an event sample in an opened stream
---

# Stream Event

## Message

A `Stream Event` message represents an event sample of a resource. For example, if a server request a client resource, i.e., "temperature" without specifying interval, the client should send a `Stream Event` when considered by device, i.e, a periodical interval defined by its own, when the value changes significantly, an event is detected, and so on.

### Header

| Field | Value | Description |
| :--- | :--- | :--- |
| **Message Type** | 0x0B | Stream Sample |
| **Message Size** | [varint](../../definitions.md#varint) | Remaining Message Length |

### Body

| Field | Identifier | Type | Mandatory | Value |
| :--- | :--- | :--- | :--- | :--- |
| **Stream Id** | 0x01 | [varint](../../definitions.md#varint) | Yes | Stream identifier. |
| **Input** | 0x02 |  | No | Current resource input. |
| **Output** | 0x03 |  | No | Current resource output. |

### Example 

TBD

