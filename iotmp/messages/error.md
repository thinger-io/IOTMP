---
description: Message to indicate an error on the previous request.
---

# Error

An [Error ](error.md)Message can be sent both by clients or servers to indicate an error on a previous request identified with its [Stream Identifier](../definitions.md#stream-identifier).

## Header

| Field            | Value                              | Description              |
| ---------------- | ---------------------------------- | ------------------------ |
| **Message Type** | 0x02                               | Error                    |
| **Message Size** | [varint](../definitions.md#varint) | Remaining Message Length |

## Body

<table><thead><tr><th>Name</th><th>Field</th><th data-type="select">Type</th><th data-type="checkbox">Mandatory</th><th>Description</th></tr></thead><tbody><tr><td><strong>Stream Id</strong></td><td>0x01</td><td></td><td>true</td><td><a href="../definitions.md#stream-identifier">Stream identifier</a> of the source request.</td></tr><tr><td><strong>Parameters</strong></td><td>0x02</td><td></td><td>false</td><td>Optional parameters associated to the response, like a response code, payload description, etc.</td></tr><tr><td><strong>Payload</strong></td><td>0x03</td><td></td><td>false</td><td>Optional payload associated to the response</td></tr></tbody></table>
