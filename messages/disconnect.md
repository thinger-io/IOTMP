---
description: Message used to cleanly disconnect a current connection.
---

# Disconnect

## Request

A `Disconnect`message can be sent anytime to close an ongoing connection. It can be initiated both by the server or the client.

Once sent or received, it is expected that the connection is closed.&#x20;

### Header

| Field            | Value                              | Description              |
| ---------------- | ---------------------------------- | ------------------------ |
| **Message Type** | 0x04                               | Disconnect               |
| **Message Size** | [varint](../definitions.md#varint) | Remaining Message Length |

### Body

<table><thead><tr><th>Name</th><th>Field</th><th data-type="select">Type</th><th data-type="checkbox">Mandatory</th><th>Description</th></tr></thead><tbody><tr><td><strong>Stream Id</strong></td><td>0x01</td><td></td><td>false</td><td>Disconnect <a href="../definitions.md#stream-identifier">Stream Identifier</a>. Not required if acknowledgement is not expected from the other side.</td></tr><tr><td><strong>Parameters</strong></td><td>0x02</td><td></td><td>false</td><td>Disconnect reason.</td></tr><tr><td><strong>Payload</strong></td><td>0x03</td><td></td><td>false</td><td>Additional disconnect information.</td></tr></tbody></table>

## Response

