---
description: Message to indicate success on the previous request.
---

# Ok

An Ok Message can be sent both by clients or servers to indicate success on a previous request identified with its [Stream Identifier](../definitions.md#stream-identifier).

## Header

<table><thead><tr><th width="191">Field</th><th width="116.33333333333331">Value</th><th>Description</th></tr></thead><tbody><tr><td><strong>Message Type</strong></td><td>0x01</td><td>Ok</td></tr><tr><td><strong>Message Size</strong></td><td><a href="../definitions.md#varint">varint</a></td><td>Remaining Message Length</td></tr></tbody></table>

## Body

<table><thead><tr><th width="163">Name</th><th width="85">Field</th><th width="93">Type<select><option value="faaeb5d050da4a2a90335311051c9a1f" label="varint" color="blue"></option><option value="fe8503ea020645ffb7798d63f1250324" label="any" color="blue"></option></select></th><th width="117" data-type="checkbox">Mandatory</th><th>Description</th></tr></thead><tbody><tr><td><strong>Stream Id</strong></td><td>0x01</td><td><span data-option="faaeb5d050da4a2a90335311051c9a1f">varint</span></td><td>true</td><td><a href="../definitions.md#stream-identifier">Stream identifier</a> of the source request.</td></tr><tr><td><strong>Parameters</strong></td><td>0x02</td><td><span data-option="fe8503ea020645ffb7798d63f1250324">any</span></td><td>false</td><td>Optional parameters associated to the response, like a response code, payload description, etc.</td></tr><tr><td><strong>Payload</strong></td><td>0x03</td><td><span data-option="fe8503ea020645ffb7798d63f1250324">any</span></td><td>false</td><td>Optional payload associated to the response</td></tr></tbody></table>

