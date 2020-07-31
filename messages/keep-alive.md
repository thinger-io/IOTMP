---
description: Message to keep the connection open
---

# Keep Alive

`Keep Alive` messages must be sent by clients at the predefined time interval. If the client fails to send the keep alive at the specified rate, the server will consider the client as disconnected and will close the on-going connection. The server must send back a `Keep Alive` message to the client as soon as received. Clients not receiving the keep alive response at the specified interval must consider the connection as broken, and re-initiate the connection mechanishm \(if required\).

## Header

| Field | Value | Description |
| :--- | :--- | :--- |
| Message Type | 0x03 | Keep Alive |
| Message Size | 0x00 | No body |

## Example

