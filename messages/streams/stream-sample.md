---
description: Message used to represent a periodical sample in an opened stream
---

# Stream Sample

## Message

A `Stream Sample` message represents a periodical sample of a resource, as configured after receiving  a `Start Stream` message. For example, if a server request a client resource "temperature" with an interval of 5 seconds, the client should send a `Stream Sample` message every 5 seconds with the content of the "temperature" resource. This message is defined as the following:

### Header

| Field | Value | Description |
| :--- | :--- | :--- |
| **Message Type** | 0x0A | Stream Sample |
| **Message Size** | [varint](../../definitions.md#varint) | Remaining Message Length |

### Body

| Field | Identifier | Type | Mandatory | Value |
| :--- | :--- | :--- | :--- | :--- |
| **Stream Id** | 0x01 | [varint](../../definitions.md#varint) | Yes | Stream identifier. |
| **Input** | 0x02 |  | No | Current resource input. |
| **Output** | 0x03 |  | No | Current resource output. |

### Example 

TBD

