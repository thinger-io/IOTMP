---
description: Message to authenticate and negotiate connection parameters.
---

# Connect

## Request

A [Connect ](connect.md)message MUST be sent from the client to the server to authenticate and negotiate the connection parameters. This message MUST be the first one after establishing the connection. If any other message or data is received, the server MUST close the connection immediately.

### Header

| Field            | Value                              | Description              |
| ---------------- | ---------------------------------- | ------------------------ |
| **Message Type** | 0x03                               | Connect                  |
| **Message Size** | [varint](../definitions.md#varint) | Remaining Message Length |

### Body

<table><thead><tr><th>Name</th><th>Field</th><th data-type="select">Type</th><th data-type="checkbox">Mandatory</th><th>Description</th></tr></thead><tbody><tr><td><strong>Stream Id</strong></td><td>0x01</td><td></td><td>true</td><td>Connect <a href="../definitions.md#stream-identifier">Stream identifier</a>.</td></tr><tr><td><strong>Parameters</strong></td><td>0x02</td><td></td><td>false</td><td><del>Connect parameters, that can be used to identify the authentication type.</del></td></tr><tr><td><strong>Payload</strong></td><td>0x03</td><td></td><td>true</td><td>Authentication payload to log-in with the server.</td></tr><tr><td><del><strong>Keep Alive</strong></del></td><td>0x04</td><td></td><td>false</td><td>Establish a Keep Alive interval in seconds. Default keep-alive interval depends on server implementation. </td></tr><tr><td><del><strong>Encoding</strong></del></td><td>0x05</td><td></td><td>false</td><td>Defines the encoding mechanism that will be used when sending <a href="../definitions.md#any">any</a> values</td></tr><tr><td><del><strong>Version</strong></del></td><td>0x06</td><td></td><td>false</td><td>Specifies the protocol version to be used.</td></tr></tbody></table>

## Response

