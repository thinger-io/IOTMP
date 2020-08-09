---
description: Message to discover available resources in endpoints
---

# Describe Resources

This message enables discovering remote [resources ](../definitions.md#resources)defined both in client and server. Resources can be defined dynamically by clients and servers. As described in the [resources ](../definitions.md#resources)definition, a resource is basically like a function that can be executed like in RPC \(Remote Procedure Call\). As a "function" it can receive parameters, inputs, and provide an output. 

This message allows discovering such resources, like its names, function type, if they support streaming, require parameters, etc.

## Request

### Header

| Field | Value | Description |
| :--- | :--- | :--- |
| **Message Type** | 0x07 | Describe Resources |
| **Message Size** | [varint](../definitions.md#varint) | Remaining Message Length |

### Body

| Field | Identifier | Type | Mandatory | Value |
| :--- | :--- | :--- | :--- | :--- |
| **Stream Id** | 0x01 | [varint](../definitions.md#varint) | Yes | [Stream identifier](../definitions.md#stream-identifier). |
| **Resource**  | 0x02 |  | No | [Resource identifier](../definitions.md#resource-definition).  |

## Response \(Resources\)

### Ok

If the request succeed, the endpoint should return an OK message with the following fields:

| Field | Identifier | Type | Mandatory | Value |
| :--- | :--- | :--- | :--- | :--- |
| **Stream Id** | 0x01 | [varint](../definitions.md#varint) | Yes | [Stream identifier](../definitions.md#stream-identifier) used in the request. |
| **Payload** | 0x03 |  | Yes | Document describing the resource. |

The payload should contain a document with the following format:

```javascript
{
  "relay": {
    "fn": 2
    "id": 0
  },
  "temperature": {
    "fn": 3
    "id": 1
  },
  "reset" : {
    "fn": 1,
    "st": false,
    "id": 2
}
```

In such document each key represents the resource name

<table>
  <thead>
    <tr>
      <th style="text-align:left">Describe Field</th>
      <th style="text-align:left">Key</th>
      <th style="text-align:left">Value</th>
      <th style="text-align:left">Mandatory</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">Function Type</td>
      <td style="text-align:left">fn</td>
      <td style="text-align:left">
        <p>1 : function without parameters</p>
        <p>2 : function with input</p>
        <p>3: function with output</p>
        <p>4: function with input and output</p>
      </td>
      <td style="text-align:left">Yes</td>
      <td style="text-align:left">Provides information about the function type, i.e., if it requires and
        input, provides an output, none, or both of them.</td>
    </tr>
    <tr>
      <td style="text-align:left">Parameters</td>
      <td style="text-align:left">pr</td>
      <td style="text-align:left">
        <p>true: requires parameters</p>
        <p>false: no parameters required</p>
      </td>
      <td style="text-align:left">No</td>
      <td style="text-align:left">Determines if the resource requires parameters to be executed. By default,
        if not specified, the resource does not require parameters to be executed.</td>
    </tr>
    <tr>
      <td style="text-align:left">Stream</td>
      <td style="text-align:left">st</td>
      <td style="text-align:left">
        <p>true : support Stream</p>
        <p>false: no stream support</p>
      </td>
      <td style="text-align:left">No</td>
      <td style="text-align:left">Determines if the resource can be used with the Streams functionality.
        By default, if not specified, the stream support is enabled.</td>
    </tr>
    <tr>
      <td style="text-align:left">Resource identifier</td>
      <td style="text-align:left">id</td>
      <td style="text-align:left">varint</td>
      <td style="text-align:left">No</td>
      <td style="text-align:left">An alternative numeric resource identifier, instead of a name, that can
        be used to call this resource.</td>
    </tr>
  </tbody>
</table>

### Error

The resources cannot be described, i.e., no support for describing resources.

## Response \(Resource\)

### Ok

If the request succeed, the endpoint should return an OK message with the following fields:

| Field | Identifier | Type | Mandatory | Value |
| :--- | :--- | :--- | :--- | :--- |
| **Stream Id** | 0x01 | [varint](../definitions.md#varint) | Yes | [Stream identifier](../definitions.md#stream-identifier) used in the request. |
| **Resource Input** | 0x04 |  | No | Document describing the resource input. |
| **Resource Output** | 0x05 |  | No | Document describing the resource output. |
| **Parameters** | 0x06 |  | No | Document describing the resource parameters. |

### Error

The resource cannot be described, i.e, it does not exists.

