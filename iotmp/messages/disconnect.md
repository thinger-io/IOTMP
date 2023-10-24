---
description: Message used to cleanly disconnect a current connection.
---

# Disconnect

## Request

A `Disconnect`message can be sent anytime to close an ongoing connection. It can be initiated both by the server or the client.

Once sent or received, it is expected that the connection is closed.&#x20;

### Header

<table><thead><tr><th width="171">Field</th><th width="83.33333333333331">Value</th><th>Description</th></tr></thead><tbody><tr><td><strong>Message Type</strong></td><td>0x04</td><td>Disconnect</td></tr><tr><td><strong>Message Size</strong></td><td><a href="../definitions.md#varint">varint</a></td><td>Remaining Message Length</td></tr></tbody></table>

### Body

<table><thead><tr><th width="165">Name</th><th width="98">Field</th><th width="100" data-type="select">Type</th><th width="120" data-type="checkbox">Mandatory</th><th>Description</th></tr></thead><tbody><tr><td><strong>Stream Id</strong></td><td>0x01</td><td></td><td>false</td><td>Disconnect <a href="../definitions.md#stream-identifier">Stream Identifier</a>. Not required if acknowledgement is not expected from the other side.</td></tr><tr><td><strong>Parameters</strong></td><td>0x02</td><td></td><td>false</td><td>Disconnect reason.</td></tr><tr><td><strong>Payload</strong></td><td>0x03</td><td></td><td>false</td><td>Additional disconnect information.</td></tr></tbody></table>

## Response

