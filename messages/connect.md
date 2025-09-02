---
description: Message to authenticate and negotiate connection parameters.
---

# Connect

## Request

A [Connect ](connect.md)message MUST be sent from the client to the server to authenticate and negotiate the connection parameters. This message MUST be the first one after establishing the connection. If any other message or data is received, the server MUST close the connection immediately.

### Header

<table><thead><tr><th width="187.33333333333331">Field</th><th width="113">Value</th><th>Description</th></tr></thead><tbody><tr><td><strong>Message Type</strong></td><td>0x03</td><td>Connect</td></tr><tr><td><strong>Message Size</strong></td><td><a href="../definitions.md#varint">varint</a></td><td>Remaining Message Length</td></tr></tbody></table>

### Body

<table><thead><tr><th width="154">Name</th><th width="80">Field</th><th width="87">Type<select><option value="ea193d2ddd7f48eca68a517c3f5feb01" label="any" color="blue"></option><option value="373c47abb07d42ea817dd87cd33c01bf" label="varint" color="blue"></option></select></th><th width="120" data-type="checkbox">Mandatory</th><th>Description</th></tr></thead><tbody><tr><td><strong>Stream Id</strong></td><td>0x01</td><td><span data-option="373c47abb07d42ea817dd87cd33c01bf">varint</span></td><td>true</td><td>Connect <a href="../definitions.md#stream-identifier">Stream identifier</a>.</td></tr><tr><td><strong>Parameters</strong></td><td>0x02</td><td><span data-option="ea193d2ddd7f48eca68a517c3f5feb01">any</span></td><td>false</td><td><del>Connect parameters, that can be used to identify the authentication type.</del></td></tr><tr><td><strong>Payload</strong></td><td>0x03</td><td><span data-option="ea193d2ddd7f48eca68a517c3f5feb01">any</span></td><td>true</td><td>Authentication payload to log-in with the server.</td></tr></tbody></table>

#### Parameters

<table><thead><tr><th width="96.26171875">Key</th><th width="100.109375">Type</th><th width="108.53125">Default</th><th>Description</th></tr></thead><tbody><tr><td>"pv"</td><td>number</td><td>0</td><td><p><strong>Protocol Version</strong></p><p>0: Legacy PSON encoding</p><p>1:  New PSON encoding (more efficient)</p></td></tr><tr><td>"ka"</td><td>number</td><td>60</td><td><p><strong>Keep-Alive Interval</strong></p><p>Heartbeat interval in seconds (max: 1800)</p><p>Server applies 15% margin for timeout detection</p></td></tr><tr><td>"at"</td><td>number</td><td>0</td><td><p><strong>Authentication Type</strong></p><p>0: Credentials (username/device/password)</p><p>Future: </p><p>1 (Auto-provision), </p><p>2 (Token), etc.</p></td></tr><tr><td>"ct"</td><td>string</td><td>-</td><td><p><strong>Client Type (future)</strong></p><p>Platform identifier: "arduino", "esp32", "raspberry", etc.</p></td></tr><tr><td>"fw"</td><td>string</td><td>-</td><td><p><strong>Firmware Version (future)</strong></p><p>Client firmware version for compatibility checks</p></td></tr></tbody></table>

Example PARAMETERS

<pre><code>{
    "pv": 1, // Use new PSON protocol
<strong>    "ka": 120, // 2-minute keep-alive
</strong>    "at": 0 // Credentials authentication
}
</code></pre>

#### Payload

The PAYLOAD field format depends on the authentication type ("at" parameter).

Authentication Type 0: Credentials (Default)

When "at": 0 or not specified, PAYLOAD must be a JSON array with exactly 3 elements:

\["username", "device\_id", "password"]

Credentials

| Index | Type   | Description           |
| ----- | ------ | --------------------- |
| 0     | string | Account username      |
| 1     | string | Device identifier     |
| 2     | string | Device password/token |

## Response

