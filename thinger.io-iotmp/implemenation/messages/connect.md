---
description: Message to authenticate and negotiate connection parameters.
---

# Connect

## Request

In the Thinger.io server implementation, there are the following default values and parameters:

<table><thead><tr><th width="204">Field</th><th width="112" data-type="select">Type</th><th width="105" data-type="checkbox">Required</th><th>Value</th></tr></thead><tbody><tr><td><strong>Stream Id</strong><br>(0x01)</td><td></td><td>true</td><td>Connect stream identifier</td></tr><tr><td><p><strong>Parameters</strong> </p><p>(0x02)</p></td><td></td><td>false</td><td><p><strong>1</strong>: Payload contains an array with username, device, and credentials</p><p></p><p><strong>2</strong>: Auth Info contains a string with a token.</p><p></p><p><strong>Default: 1 (Username/Password Credentials)</strong></p></td></tr><tr><td><strong>Payload</strong><br><strong>(0x03)</strong></td><td></td><td>true</td><td><p><strong>Parameter with value 1:</strong></p><p>Auth Info contains an array with ["username", "device", "credential"].</p><p></p><p><strong>Parameter with value 2:</strong><br>Auth Info contains a string with a token.</p></td></tr><tr><td><strong>Keep Alive Interval</strong><br><strong>(0x04)</strong></td><td></td><td>false</td><td><p>Number of expected seconds between keep alives.</p><p></p><p><strong>Default: 60 seconds</strong></p></td></tr><tr><td><strong>Payload Encoding</strong><br><strong>(0x05)</strong></td><td></td><td>false</td><td><p>0x00: Reserved  </p><p>0x01: PSON</p><p>0x02: JSON</p><p>0x03: MessagePack</p><p>0x04: BSON</p><p>0x05: CBOR</p><p>0x06: UBJSON</p><p><strong>Default: 0x01 (PSON)</strong></p></td></tr></tbody></table>

## Response

### OK

<table data-header-hidden><thead><tr><th width="163.33333333333331">Field</th><th>Type</th><th>Description</th></tr></thead><tbody><tr><td>Field</td><td>Type</td><td>Description</td></tr><tr><td>OK</td><td><p>Parameters: None</p><p>Payload: None</p></td><td>The server agree the Connect </td></tr><tr><td></td><td></td><td></td></tr><tr><td></td><td></td><td></td></tr><tr><td></td><td></td><td></td></tr></tbody></table>

### Error

<table><thead><tr><th>Error</th><th width="141" align="center">Parameter</th><th width="157">Payload</th><th>Description</th></tr></thead><tbody><tr><td><strong>Unknown</strong></td><td align="center">N/A</td><td>N/A</td><td>The server refuses the connection.</td></tr><tr><td><strong>Redirect</strong></td><td align="center">1</td><td>Target server redirect</td><td><p>The server requires the device to connect to another host, i.e., for load balancing, route to a nearest host, etc.</p><p><strong>Examples:</strong></p><p>iotmp://newserver.io</p><p>iotmps://newserver.io</p></td></tr><tr><td><strong>Bad Credentials</strong></td><td align="center">2</td><td></td><td>The provided credentials are not valid in the server.</td></tr><tr><td><strong>Invalid Keep Alive</strong></td><td align="center">3</td><td></td><td>The negotiated keep-alive is incorrect.</td></tr><tr><td><strong>Bad Encoding</strong></td><td align="center">4</td><td></td><td>The negotiated encoding is not supported by the server.</td></tr></tbody></table>
