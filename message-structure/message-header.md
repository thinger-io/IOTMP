---
description: IOTMP Message Header
---

# Message Header

The **header** is the mandatory first part of every IOTMP message. It provides the essential metadata required to parse the message:

* **Message Type** – identifies the purpose of the message.
* **Message Size** – defines the length of the message body in bytes (excluding the header).

The header is encoded using **varint fields**, resulting in a **minimum size of 2 bytes**.

<table><thead><tr><th width="179">Field</th><th width="111">Type</th><th width="134">Mandatory</th><th>Description</th></tr></thead><tbody><tr><td><a href="message-header.md#message-type"><strong>Message Type</strong></a></td><td><a href="../definitions.md#varint">varint</a></td><td>Yes</td><td>Specifies the <a href="message-header.md#message-types">Message Type</a>. </td></tr><tr><td><a href="message-header.md#message-size"><strong>Message Size</strong></a></td><td><a href="../definitions.md#varint">varint</a></td><td>Yes</td><td>Specifies the <a href="message-header.md#message-size">Message Size</a>, without taking into account the header size.</td></tr></tbody></table>

## Message Type

The **Message Type** field identifies the purpose of the IOTMP message. It is always present in the header and is encoded as a **varint**.

Message types define the control flow of the protocol, covering actions such as connection management, resource execution, error handling, and data streaming.

The protocol reserves specific numeric values for core operations, while leaving others available for future extensions. This ensures both **compatibility** and **extensibility** as new functionality is introduced.

The currently defined message types are:

<table><thead><tr><th width="229">Message Type</th><th width="130.33333333333331">Value</th><th>Description</th></tr></thead><tbody><tr><td><strong>Reserved</strong></td><td>0x00</td><td>Reserved field, not used</td></tr><tr><td><a href="../messages/ok.md"><strong>Ok</strong></a></td><td>0x01</td><td>Acknowledges success</td></tr><tr><td><a href="../messages/error.md"><strong>Error</strong></a></td><td>0x02</td><td>Indicates an error occurred</td></tr><tr><td><a href="../messages/connect.md"><strong>Connect</strong></a></td><td>0x03</td><td>Initiates a connection and specifies its parameters</td></tr><tr><td><a href="../messages/disconnect.md"><strong>Disconnect</strong></a></td><td>0x04</td><td>Terminates the current connection</td></tr><tr><td><a href="../messages/keep-alive.md"><strong>Keep Alive</strong></a></td><td>0x05</td><td>Keep the connection open</td></tr><tr><td><a href="../messages/run.md"><strong>Run Resource</strong></a></td><td>0x06</td><td>Execute a specific resource on the client or server</td></tr><tr><td><a href="../messages/describe.md"><strong>Describe Resources</strong></a></td><td>0x07</td><td>Request a description of available resources</td></tr><tr><td><a href="../messages/streams/start-stream.md"><strong>Start Stream</strong></a></td><td>0x08</td><td>Starts a stream on the specified resource</td></tr><tr><td><a href="../messages/streams/stop-stream.md"><strong>Stop Stream</strong></a></td><td>0x09</td><td>Stops an active stream</td></tr><tr><td><a href="../messages/streams/stream-event.md"><strong>Stream Data</strong></a></td><td>0x0A</td><td>Transmits data for an active stream</td></tr></tbody></table>

## Message Size

The **Message Size** field specifies the length of the message body, expressed in **bytes**. It does **not** include the size of the header itself.

* Encoded as a **varint**.
* Always present in the message header.
* A value of **0** indicates that the message has no body (only a header).

This field enables the receiver to determine exactly how many bytes to read for the payload and when a message is complete.
