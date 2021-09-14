---
description: Description of IOTMP message header.
---

# Message Header

Each IOTMP message contains a header that describes the[ Type](message-header.md#message-type) and its [Size ](message-header.md#message-size)over the wire. The minimum header length is 2 bytes.

| Field | Type | Mandatory | Description |
| :--- | :--- | :--- | :--- |
| **Message Type** | [varint](../definitions.md#varint) | Yes | Specifies the [Message Type](message-header.md#message-types).  |
| **Message Size** | [varint](../definitions.md#varint) | Yes | Specifies the [Message Size](message-header.md#message-size), without taking into account the header size. |

## Message Type

A message type can be any of the following:

| Message Type | Value | Description |
| :--- | :--- | :--- |
| **Reserved** | 0x00 | Reserved field |
| \*\*\*\*[**Ok**](../messages/ok.md)\*\*\*\* | 0x01 | Success |
| \*\*\*\*[**Error**](../messages/error.md)\*\*\*\* | 0x02 | Error |
| [**Connect**](../messages/connect.md)\*\*\*\* | 0x03 | Initiates a connection and its parameters |
| \*\*\*\*[**Disconnect**](../messages/disconnect.md)\*\*\*\* | 0x04 | Disconnect the current connection |
| \*\*\*\*[**Keep Alive**](../messages/keep-alive.md)\*\*\*\* | 0x05 | Keep connection alive |
| \*\*\*\*[**Run Resource**](../messages/run.md)\*\*\*\* | 0x06 | Execute a resource |
| \*\*\*\*[**Describe Resources**](../messages/describe.md)\*\*\*\* | 0x07 | Describe available resources |
| \*\*\*\*[**Start Stream**](../messages/streams/start-stream.md)\*\*\*\* | 0x08 | Start a stream on the specified resource |
| \*\*\*\*[**Stop Stream**](../messages/streams/stop-stream.md)\*\*\*\* | 0x09 | Stop the ongoing stream |
| \*\*\*\*[**Stream Data**](../messages/streams/stream-event.md)\*\*\*\* | 0x0A | Stream data |

## Message Size

This field specifies the message size in bytes, that is, the remaining number of bytes on the stream \(including zero if the message has no remaining bytes\).

