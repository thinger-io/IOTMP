---
description: Message to authenticate and negotiate connection parameters.
---

# Connect

## Request

A [Connect ](connect.md)message MUST be sent from the client to the server to authenticate and negotiate the connection parameters. This message MUST be the first one after establishing the connection. If any other message or data is received, the server MUST close the connection immediately.

### Header

| Field | Value | Description |
| :--- | :--- | :--- |
| **Message Type** | 0x03 | Connect |
| **Message Size** | [varint](../definitions.md#varint) | Remaining Message Length |

### Body

| Name | Field | Type | Mandatory | Description |
| :--- | :--- | :--- | :--- | :--- |
| **Stream Id** | 0x01 | [varint](../definitions.md#varint) | Yes | Connect [Stream identifier](../definitions.md#stream-identifier). |
| **Parameters** | 0x02 | [any](../definitions.md#any) | No | Connect parameters, that can be used to identify the authentication type. |
| **Credentials** | 0x03 | [any](../definitions.md#stream) | Yes | Authentication payload to log-in with the server. |
| **Keep Alive** | 0x04 | [varint](../definitions.md#varint) | No | Establish a Keep Alive interval in seconds. |
| **Encoding** | 0x05 | [any](../definitions.md#any) | No | Defines the encoding mechanism that will be used when sending fields with Wire-Type of 0x06 \(Negotiated Encoding\) |
| **Version** | 0x06 | [varint](../definitions.md#varint) | No | Specifies the protocol version to be used. |

## Response

| Message | Description |
| :--- | :--- |
| \*\*\*\*[**Ok**](ok.md)\*\*\*\* | The server should answer with an OK if it is able to authenticate the client and the negotiated parameters are acceptable. It must contain the Stream Id specified in this message. |
| \*\*\*\*[**Error**](error.md)\*\*\*\* | The server should answer with an Error if it is not able to authenticate the client or the negotiated parameters are not acceptable. It must contain the Stream Id specified in this message. |

## Thinger.io

### Request

In the Thinger.io server implementation, there are the following default values and parameters:

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
      <td style="text-align:left"><b>Parameters</b>
      </td>
      <td style="text-align:left">&lt;b&gt;&lt;/b&gt;<a href="../definitions.md#varint">varint</a>
      </td>
      <td style="text-align:left">
        <p>1: Auth Info contains an array with [&quot;username&quot;, &quot;device&quot;,
          &quot;credential&quot;].</p>
        <p>2: Auth Info contains a string with a token.</p>
        <p><b>Default: 1 (Username/Password Credentials)</b>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Keep Alive Interval</b>
      </td>
      <td style="text-align:left"><a href="../definitions.md#varint">varint</a>
      </td>
      <td style="text-align:left">
        <p>Number of expected seconds between keep alives.</p>
        <p><b>Default: 60 seconds</b>
        </p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Payload Encoding</b>
      </td>
      <td style="text-align:left"><a href="../definitions.md#varint">varint</a>
      </td>
      <td style="text-align:left">
        <p>0x00: Reserved</p>
        <p>0x01: PSON</p>
        <p>0x02: JSON</p>
        <p>0x03: MessagePack</p>
        <p>0x04: BSON</p>
        <p>0x05: CBOR</p>
        <p>0x06: UBJSON</p>
        <p><b>Default: 0x01 (PSON)</b>
        </p>
      </td>
    </tr>
  </tbody>
</table>

### Response Ok

<table>
  <thead>
    <tr>
      <th style="text-align:left">Field</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">OK</td>
      <td style="text-align:left">
        <p>Parameters: None</p>
        <p>Payload: None</p>
      </td>
      <td style="text-align:left">The server agree the Connect</td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
    <tr>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
      <td style="text-align:left"></td>
    </tr>
  </tbody>
</table>

### Response Error

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
      <td style="text-align:left"><b>Unknown</b>
      </td>
      <td style="text-align:left"></td>
      <td style="text-align:left">The server</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Redirect</b>
      </td>
      <td style="text-align:left">
        <p>Parameters: 1</p>
        <p>Payload: Server to connect</p>
      </td>
      <td style="text-align:left">
        <p>The server requires the device to connect to another host, i.e., for load
          balancing, route to a nearest host, etc.</p>
        <p><b>Examples:</b>
        </p>
        <p>iotmp://newserver.io</p>
        <p>iotmps://newserver.io</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Bad Credentials</b>
      </td>
      <td style="text-align:left">Parameters: 2</td>
      <td style="text-align:left">The provided credentials are not valid in the server.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Invalid Keep Alive</b>
      </td>
      <td style="text-align:left">Parameters: 3</td>
      <td style="text-align:left">The negotiated keep-alive is incorrect.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Bad Encoding</b>
      </td>
      <td style="text-align:left">Parameters: 4</td>
      <td style="text-align:left">The negotiated encoding is not supported by the server.</td>
    </tr>
  </tbody>
</table>

