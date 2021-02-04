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

## Response

| Message | Description |
| :--- | :--- |
| \*\*\*\*[**Ok**](ok.md)\*\*\*\* | The server should answer with an OK if it is able to authenticate the client and the negotiated parameters are acceptable. It must contain the Stream Id specified in this message. |
| \*\*\*\*[**Error**](error.md)\*\*\*\* | The server should answer with an Error if it is not able to authenticate the client or the negotiated parameters are not acceptable. It must contain the Stream Id specified in this message. |

## Thinger.io

### Request

In Thinger.io server implementation, there are the following default values and parameters:

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
        <p><b>Default: 1</b>
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
        <p><b>Default: 60</b>
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
        <p>0x01: PSON format (Default)</p>
        <p>0x02: JSON format</p>
        <p>0x03: MessagePack format</p>
        <p>0x04: BSON format</p>
        <p>0x05: CBOR format</p>
        <p>0x06: UBJSON format</p>
      </td>
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

### Response

