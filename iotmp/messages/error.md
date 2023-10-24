---
description: Message to indicate an error on the previous request.
---

# Error

An [Error ](error.md)Message can be sent both by clients or servers to indicate an error on a previous request identified with its [Stream Identifier](../definitions.md#stream-identifier).

## Header

<table><thead><tr><th width="180.33333333333331">Field</th><th width="119">Value</th><th>Description</th></tr></thead><tbody><tr><td><strong>Message Type</strong></td><td>0x02</td><td>Error</td></tr><tr><td><strong>Message Size</strong></td><td><a href="../definitions.md#varint">varint</a></td><td>Remaining Message Length</td></tr></tbody></table>

## Body

<table><thead><tr><th width="156">Name</th><th width="120">Field</th><th width="92" data-type="select">Type</th><th width="125" data-type="checkbox">Mandatory</th><th>Description</th></tr></thead><tbody><tr><td><strong>Stream Id</strong></td><td>0x01</td><td></td><td>true</td><td><a href="../definitions.md#stream-identifier">Stream identifier</a> of the source request.</td></tr><tr><td><strong>Parameters</strong></td><td>0x02</td><td></td><td>false</td><td>Optional parameters associated to the response, like a response code, payload description, etc.</td></tr><tr><td><strong>Payload</strong></td><td>0x03</td><td></td><td>false</td><td>Optional payload associated to the response</td></tr></tbody></table>
