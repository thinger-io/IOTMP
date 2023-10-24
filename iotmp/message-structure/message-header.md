---
description: IOTMP Message Header
---

# Message Header

The **header** is a part of a message that contains information about the type of message and the size of the data being transmitted.

Each IOTMP message contains a header that describes the[ Type](message-header.md#message-type) and its [Size ](message-header.md#message-size)over the wire. The minimum header length is 2 bytes.

<table><thead><tr><th width="179">Field</th><th width="111">Type</th><th width="134">Mandatory</th><th>Description</th></tr></thead><tbody><tr><td><a href="message-header.md#message-type"><strong>Message Type</strong></a></td><td><a href="../definitions.md#varint">varint</a></td><td>Yes</td><td>Specifies the <a href="message-header.md#message-types">Message Type</a>. </td></tr><tr><td><a href="message-header.md#message-size"><strong>Message Size</strong></a></td><td><a href="../definitions.md#varint">varint</a></td><td>Yes</td><td>Specifies the <a href="message-header.md#message-size">Message Size</a>, without taking into account the header size.</td></tr></tbody></table>

## Message Type

A message type can be any of the following:

<table><thead><tr><th width="229">Message Type</th><th width="130.33333333333331">Value</th><th>Description</th></tr></thead><tbody><tr><td><strong>Reserved</strong></td><td>0x00</td><td>Reserved field</td></tr><tr><td><a href="../messages/ok.md"><strong>Ok</strong></a></td><td>0x01</td><td>Success</td></tr><tr><td><a href="../messages/error.md"><strong>Error</strong></a></td><td>0x02</td><td>Error</td></tr><tr><td><a href="../messages/connect.md"><strong>Connect</strong></a></td><td>0x03</td><td>Initiates a connection and its parameters</td></tr><tr><td><a href="../messages/disconnect.md"><strong>Disconnect</strong></a></td><td>0x04</td><td>Disconnect the current connection</td></tr><tr><td><a href="../messages/keep-alive.md"><strong>Keep Alive</strong></a></td><td>0x05</td><td>Keep connection alive</td></tr><tr><td><a href="../messages/run.md"><strong>Run Resource</strong></a></td><td>0x06</td><td>Execute a resource</td></tr><tr><td><a href="../messages/describe.md"><strong>Describe Resources</strong></a></td><td>0x07</td><td>Describe available resources</td></tr><tr><td><a href="../messages/streams/start-stream.md"><strong>Start Stream</strong></a></td><td>0x08</td><td>Start a stream on the specified resource</td></tr><tr><td><a href="../messages/streams/stop-stream.md"><strong>Stop Stream</strong></a></td><td>0x09</td><td>Stop the ongoing stream</td></tr><tr><td><a href="../messages/streams/stream-event.md"><strong>Stream Data</strong></a></td><td>0x0A</td><td>Stream data</td></tr></tbody></table>

## Message Size

This field specifies the message size in bytes, that is, the remaining number of bytes on the stream (including zero if the message has no remaining bytes).
