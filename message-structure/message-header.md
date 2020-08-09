---
description: Description of IOTMP message header.
---

# Message Header

Each IOTMP message contains a header that describes the [Message Type](message-header.md#message-type) and its length over the wire. The minimum header length is 2 bytes.

| Field | Type | Description |
| :--- | :--- | :--- |
| **Message Type** | [varint](../definitions.md#varint) | Specifies the [Message Type](message-header.md#message-types).  |
| **Remaining Length** | [varint](../definitions.md#varint) | Specifies the remaining bytes of the message, without taking into account the header. |

## Message Type

| Message Type | Value | Description |
| :--- | :--- | :--- |
| **Reserved** | 0x00 | Reserved field |
| \*\*\*\*[**Ok**](../messages/ok.md)\*\*\*\* | 0x01 | Success |
| \*\*\*\*[**Error**](../messages/error.md)\*\*\*\* | 0x02 | Error |
| [**Connect**](../messages/connect.md)\*\*\*\* | 0x03 | Establish a connection and its parameters |
| \*\*\*\*[**Disconnect**](../messages/disconnect.md)\*\*\*\* | 0x04 | Disconnect the current connection |
| \*\*\*\*[**Keep Alive**](../messages/keep-alive.md)\*\*\*\* | 0x05 | Keep connection alive |
| \*\*\*\*[**Run Resource**](../messages/run.md)\*\*\*\* | 0x06 | Execute a resource on the target endpoint |
| \*\*\*\*[**Describe Resources**](../messages/describe.md)\*\*\*\* | 0x07 | Describe available resources on the target endpoint |
| \*\*\*\*[**Start Stream**](../messages/streams/start-stream.md)\*\*\*\* | 0x08 | Start a stream for receiving updates on a specific resource |
| \*\*\*\*[**Stop Stream**](../messages/streams/stop-stream.md)\*\*\*\* | 0x09 | Stop the ongoing stream |
| \*\*\*\*[**Stream Event**](../messages/streams/stream-event.md)\*\*\*\* | 0x0A | Stream event |
| \*\*\*\*[**Stream Sample**](../messages/streams/stream-sample.md)\*\*\*\* | 0x0B | Stream a scheduled sample |

## Remaining Length

