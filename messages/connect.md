---
description: Message to authenticate and negotiate connection parameters.
---

# Connect

## Request

A [Connect ](connect.md)message MUST be sent from the client to the server to authenticate and negotiate the connection parameters. This message MUST be the first one after establishing the connection. If any other message or data is received, the server MUST close the connection immediately.

### Header

<table><thead><tr><th width="187.33333333333331">Field</th><th width="113">Value</th><th>Description</th></tr></thead><tbody><tr><td><strong>Message Type</strong></td><td>0x03</td><td>Connect</td></tr><tr><td><strong>Message Size</strong></td><td><a href="../definitions.md#varint">varint</a></td><td>Remaining Message Length</td></tr></tbody></table>

### Body

<table><thead><tr><th width="154">Name</th><th width="80">Field</th><th width="87">Type<select><option value="ea193d2ddd7f48eca68a517c3f5feb01" label="any" color="blue"></option><option value="373c47abb07d42ea817dd87cd33c01bf" label="varint" color="blue"></option></select></th><th width="120" data-type="checkbox">Mandatory</th><th>Description</th></tr></thead><tbody><tr><td><strong>Stream Id</strong></td><td>0x01</td><td><span data-option="373c47abb07d42ea817dd87cd33c01bf">varint</span></td><td>true</td><td>Connect <a href="../definitions.md#stream-identifier">Stream identifier</a>.</td></tr><tr><td><strong>Parameters</strong></td><td>0x02</td><td><span data-option="ea193d2ddd7f48eca68a517c3f5feb01">any</span></td><td>false</td><td><del>Connect parameters, that can be used to identify the authentication type.</del></td></tr><tr><td><strong>Payload</strong></td><td>0x03</td><td><span data-option="ea193d2ddd7f48eca68a517c3f5feb01">any</span></td><td>true</td><td>Authentication payload to log-in with the server.</td></tr><tr><td><del><strong>Keep Alive</strong></del></td><td>0x04</td><td><span data-option="373c47abb07d42ea817dd87cd33c01bf">varint</span></td><td>false</td><td>Establish a Keep Alive interval in seconds. Default keep-alive interval depends on server implementation. </td></tr><tr><td><del><strong>Encoding</strong></del></td><td>0x05</td><td><span data-option="ea193d2ddd7f48eca68a517c3f5feb01">any</span></td><td>false</td><td>Defines the encoding mechanism that will be used when sending <a href="../definitions.md#any">any</a> values</td></tr><tr><td><del><strong>Version</strong></del></td><td>0x06</td><td><span data-option="ea193d2ddd7f48eca68a517c3f5feb01">any</span></td><td>false</td><td>Specifies the protocol version to be used.</td></tr></tbody></table>

## Response

