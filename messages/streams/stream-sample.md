---
description: Message used to represent a periodical sample in an opened stream
---

# Stream Sample

## Message

A `Stream Sample` message represents a periodical sample of a resource, as configured after receiving  a `Start Stream` message. For example, if a server request a client resource "temperature" with an interval of 5 seconds, the client should send a `Stream Sample` message every 5 seconds with the content of the "temperature" resource. This message is defined as the following:

### Header

| Field | Value | Description |
| :--- | :--- | :--- |
| **Message Type** | 0x0B | Stream Sample |
| **Message Size** | varint | Remaining Message Length |

### Body

| Field | Identifier | Type | Mandatory | Value |
| :--- | :--- | :--- | :--- | :--- |
| **Stream Id** | 0x01 | varint | Yes | Stream identifier. |
| **Payload** | 0x03 |  | Yes | Content of the resource to be streamed. |

### Example 

TBD

