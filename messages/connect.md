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

<table>
  <thead>
    <tr>
      <th style="text-align:left">Name</th>
      <th style="text-align:left">Field</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Mandatory</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>Stream Id</b>
      </td>
      <td style="text-align:left">0x01</td>
      <td style="text-align:left"><a href="../definitions.md#varint">varint</a>
      </td>
      <td style="text-align:left">Yes</td>
      <td style="text-align:left">Connect <a href="../definitions.md#stream-identifier">Stream identifier</a>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Parameters</b>
      </td>
      <td style="text-align:left">0x02</td>
      <td style="text-align:left"><a href="../definitions.md#any">any</a>
      </td>
      <td style="text-align:left">No</td>
      <td style="text-align:left">Connect parameters, that can be used to identify the authentication type.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Credentials</b>
      </td>
      <td style="text-align:left">0x03</td>
      <td style="text-align:left"><a href="../definitions.md#stream">any</a>
      </td>
      <td style="text-align:left">Yes</td>
      <td style="text-align:left">Authentication payload to log-in with the server.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Keep Alive</b>
      </td>
      <td style="text-align:left">0x04</td>
      <td style="text-align:left"><a href="../definitions.md#varint">varint</a>
      </td>
      <td style="text-align:left">No</td>
      <td style="text-align:left">
        <p>Establish a Keep Alive interval in seconds.</p>
        <p><b>e</b>N0x05</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Encoding</b>
      </td>
      <td style="text-align:left">0x05</td>
      <td style="text-align:left"><a href="../definitions.md#varint">varint</a>
      </td>
      <td style="text-align:left">No</td>
      <td style="text-align:left">Defines the encoding mechanism that will be used for encoding <a href="../definitions.md#any">any </a>fields
        sent along the communication.</td>
    </tr>
  </tbody>
</table>

## Response

| Message | Description |
| :--- | :--- |
| \*\*\*\*[**Ok**](ok.md)\*\*\*\* | The server should answer with an OK if it is able to authenticate the client and the negotiated parameters are acceptable. It must contain the Stream Id specified in this message. |
| \*\*\*\*[**Error**](error.md)\*\*\*\* | The server should answer with an Error if it is not able to authenticate the client or the negotiated parameters are not acceptable. It must contain the Stream Id specified in this message. |

## 

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
        <p>0x01: PSON format</p>
        <p>0x02: JSON format</p>
        <p>0x03: MessagePack format</p>
        <p>0x04: BSON format</p>
        <p>0x05: CBOR format</p>
        <p>0x06: UBJSON format</p>
        <p><b>Default: 0x01 PSON</b>
        </p>
      </td>
    </tr>
  </tbody>
</table>

### Response

