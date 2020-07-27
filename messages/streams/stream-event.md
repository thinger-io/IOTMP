---
description: Message used to represent an event sample in an opened stream
---

# Stream Event

## Message

A `Stream Event` message represents an event sample of a resource. For example, if a server request a client resource "temperature" without specifying interval, the client should send a `Stream Event` when considered by device, i.e, a periodical interval define by its own, when the value change significantly, an event is detected, etc.

### Header

| Field | Value | Description |
| :--- | :--- | :--- |
| **Message Type** | 0x0A | Stream Sample |
| **Message Size** | varint | Remaining Message Length |

### Body

| Field | Identifier | Type | Mandatory | Value |
| :--- | :--- | :--- | :--- | :--- |
| **Stream Id** | 0x01 | varint | Yes | Stream identifier. |
| **Payload** | 0x03 |  | Yes | Content of the resource to be streamed. |

### Example 

TBD

