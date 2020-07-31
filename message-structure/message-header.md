---
description: Description of IOTMP message header.
---

# Message Header

Each IOTMP message contains a header that describes the message type and its length over the wire. It is basically composed by two fields: Message Type and Remaining Length. The minimum header length is 2 bytes.

| Field | Type | Description |
| :--- | :--- | :--- |
| **Message Type** | [varint](../definitions.md#varint) | Specifies the [Message Type](message-header.md#message-types).  |
| **Remaining Length** | [varint](../definitions.md#varint) | Specifies the remaining bytes of the message, without taking into account the header. |

## Message Types

| Message Type | Value | Description |
| :--- | :--- | :--- |
| **Reserved** | 0x00 | Field that cannot be used |
| **OK** | 0x01 | Success on request |
| **Error** | 0x02 | Error on request |
| **Keep Alive** | 0x03 | Keep connection alive |
| **Run Resource** | 0x04 | Execute a resource or a broker action |
| **Start Stream** | 0x05 | Start stream channel for sampling interval or receive events over a resource. |
| **Stop Stream** | 0x06 | Stop the ongoing stream |
| **Describe Resources** | 0x07 | Describe available resources |
| **Connect** | 0x08 | Establish a connection and its parameters |
| **Disconnect** | 0x09 | Disconnect the current connection |
| **Stream Event** | 0x0A | Stream an unscheduled event |
| **Stream Sample** | 0x0B | Stream an scheduled sample |

