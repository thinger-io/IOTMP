---
description: Message to authenticate a negotiate connection parameters.
---

# Connect

## Request

A `Connect` message MUST be sent from the client to the server to authenticate and negotiate the connection parameters. This message MUST be the first one after establishing the connection. If any other message or data is received, the server MUST close the connection immediately.

### Header

| Field | Value | Description |
| :--- | :--- | :--- |
| **Message Type** | 0x08 | Connect |
| **Message Size** | varint | Remaining Message Length |

### Body

| Field | Identifier | Type | Mandatory | Value |
| :--- | :--- | :--- | :--- | :--- |
| **Stream Id** | 0x01 | [varint](../definitions.md#varint) | Yes | Request Identifier. |
| **Auth Type** | 0x02 | [varint](../definitions.md#varint) | No | Depending on the value, the authentication is done over different mechanisms, like credentials, certificates, token, etc. |
| **Auth Info** | 0x03 |  | Yes | Authentication payload as defined by the `Auth Type` field. By default, the `Auth Type` is 1 \(credentials\), so the `Auth Info` MUST contain an array with the username, device identifier, and credentials.  |
| **Keep Alive** | 0x04 | varint | No | Establish a Keep Alive interval in seconds \(60 seconds by default\). |
| **Payload Encoding** | 0x05 | varint |  | Defines the encoding mechanism that will be used for encoding `Json` fields. |

### Field Values

<table>
  <thead>
    <tr>
      <th style="text-align:left">Field</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Values</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>Auth Type</b>
      </td>
      <td style="text-align:left">VARINT</td>
      <td style="text-align:left">
        <p>1: Payload contains an array with [&quot;username&quot;, &quot;device&quot;,
          &quot;credential&quot;].</p>
        <p>2: Payload contain a string with the client certificate.</p>
        <p>3: Payload contains a string with a Token.</p>
        <p><b>Default: 1</b>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Keep Alive Interval</b>
      </td>
      <td style="text-align:left">VARINT</td>
      <td style="text-align:left">
        <p>Number of expected seconds between keep alives.</p>
        <p><b>Default: 60</b>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Payload Encoding</b>
      </td>
      <td style="text-align:left">VARINT</td>
      <td style="text-align:left">
        <p>1: DATA type is encoded with PSON format</p>
        <p>2: DATA encoded with JSON format</p>
        <p>3: DATA encoded with MessagePack format</p>
        <p>4: DATA encoded with CBOR format</p>
        <p>5: DATA encoded with UBJSON format</p>
        <p><b>Default: 1</b>
        </p>
      </td>
    </tr>
  </tbody>
</table>

## Response

| Message | Description |
| :--- | :--- |
| \*\*\*\*[**Ok**](ok.md)\*\*\*\* | The server should answer with an OK if it is able to authenticate the client and the negotiated parameters are acceptable. It must contain the Stream Id specified in this message. |
| \*\*\*\*[**Error**](error.md)\*\*\*\* | The server should answer with an Error if it is not able to authenticate the client or the negotiated parameters are not acceptable. It must contain the Stream Id specified in this message. |

## Examples



