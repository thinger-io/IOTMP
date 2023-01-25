---
description: Message to authenticate and negotiate connection parameters.
---

# Connect

## Request

In the Thinger.io server implementation, there are the following default values and parameters:

<table><thead><tr><th>Field</th><th data-type="select">Type</th><th data-type="checkbox">Required</th><th>Value</th></tr></thead><tbody><tr><td><strong>Stream Id</strong><br>(0x01)</td><td></td><td>true</td><td>Connect stream identifier</td></tr><tr><td><p><strong>Parameters</strong> </p><p>(0x02)</p></td><td></td><td>false</td><td><p><strong>1</strong>: Payload contains an array with username, device, and credentials</p><p></p><p><strong>2</strong>: Auth Info contains a string with a token.</p><p></p><p><strong>Default: 1 (Username/Password Credentials)</strong></p></td></tr><tr><td><strong>Payload</strong><br><strong>(0x03)</strong></td><td></td><td>true</td><td><p><strong>Parameter with value 1:</strong></p><p>Auth Info contains an array with ["username", "device", "credential"].</p><p></p><p><strong>Parameter with value 2:</strong><br>Auth Info contains a string with a token.</p></td></tr><tr><td><strong>Keep Alive Interval</strong><br><strong>(0x04)</strong></td><td></td><td>false</td><td><p>Number of expected seconds between keep alives.</p><p></p><p><strong>Default: 60 seconds</strong></p></td></tr><tr><td><strong>Payload Encoding</strong><br><strong>(0x05)</strong></td><td></td><td>false</td><td><p>0x00: Reserved  </p><p>0x01: PSON</p><p>0x02: JSON</p><p>0x03: MessagePack</p><p>0x04: BSON</p><p>0x05: CBOR</p><p>0x06: UBJSON</p><p><strong>Default: 0x01 (PSON)</strong></p></td></tr></tbody></table>

## Response

### OK

| Field | Type                                        | Description                   |
| ----- | ------------------------------------------- | ----------------------------- |
| OK    | <p>Parameters: None</p><p>Payload: None</p> | The server agree the Connect  |
|       |                                             |                               |
|       |                                             |                               |
|       |                                             |                               |

### Error

|          Error         | Parameter | Payload                | Description                                                                                                                                                                                                       |
| :--------------------: | --------- | ---------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
|       **Unknown**      | N/A       | N/A                    | The server refuses the connection.                                                                                                                                                                                |
|      **Redirect**      | 1         | Target server redirect | <p>The server requires the device to connect to another host, i.e., for load balancing, route to a nearest host, etc.</p><p><strong>Examples:</strong></p><p>iotmp://newserver.io</p><p>iotmps://newserver.io</p> |
|   **Bad Credentials**  | 2         |                        | The provided credentials are not valid in the server.                                                                                                                                                             |
| **Invalid Keep Alive** | 3         |                        | The negotiated keep-alive is incorrect.                                                                                                                                                                           |
|    **Bad Encoding**    | 4         |                        | The negotiated encoding is not supported by the server.                                                                                                                                                           |
