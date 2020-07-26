---
description: Message to run a resource in a device or in the broker
---

# Run

This method enables running remote [resources ](../definitions.md#resources)defined both in client and server. Resources are defined dynamically by clients and devices. As described in the [resources ](../definitions.md#resources)definition, a resource is basically like a function that can be executed like in RPC \(Remote Procedure Call\). As a "function" it can receive inputs, and provide an output.

A **device** can define multiple resources as required by its use case, i.e., read humidity, adjust temperature, turn on a light, etc.  Typical resources for an IoT device are functions for reading device states, sensor values, adjust parameters, or actuating over digital pins to mention a few.

A **server** or broker can also define multiple resources that can be executed by their clients. Such resources can vary depending on the use case, and normally involves complex task that are not worth to be executed in the device. Typical resources defined by a server can be actions like writing to a database, calling an external endpoint for sending communications, managing device configuration, etc.

## Header

| Field | Value | Description |
| :--- | :--- | :--- |
| **Message Type** | 0x04 | Run |
| **Message Size** | varint | Remaining Message Length |

## Body

| Field | Identifier | Type | Value |
| :--- | :--- | :--- | :--- |
| _**Stream Id**_ | 0x01 | varint | Stream identifier to be used in the request. Can be omitted if it is not required a confirmation or a response. |
| **Resource**  | 0x02 |  | A string or array of strings with the resource identifier, i.e., "temperature". |
| _**Payload**_ | 0x03 |  | The payload sent to the target resource. Can be omitted if the target resource does not require a payload. |
| _**Action**_ | 0x04 | varint | Represent the action to be executed: i.e., run a device resource. Can be omitted, and the default action will be to execute a device resource \(0x01\) with the specified resource identifier in the `Resource` field. See [Actions](run.md#actions). |

## Default Actions

<table>
  <thead>
    <tr>
      <th style="text-align:left">Action</th>
      <th style="text-align:left">Value</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><b>Run Resource</b>
      </td>
      <td style="text-align:left">0x01</td>
      <td style="text-align:left">Run the specified resource inside the target destination, i.e, a resource
        for reading the temperature.</td>
    </tr>
    <tr>
      <td style="text-align:left"><b>Reserved</b>
      </td>
      <td style="text-align:left">
        <p>0x02</p>
        <p>0x08</p>
      </td>
      <td style="text-align:left">Reserved for future use</td>
    </tr>
  </tbody>
</table>

## Extended Actions

Any client and server can define their own functions or actions to extend the protocol functionality. This can be done by defining more values for the Action field. By default, actions from `0x01` to `0x08` are reserved, but it is possible to define several additional actions. For example, the Thinger.io implementation currently works with those extended actions:

| Action | Value | Description |
| :--- | :--- | :--- |
| **Call Endpoint** | 0x09 | Call a target endpoint, i.e., HTTP request, send an Email, Telegram, etc. |
| **Call Device** | 0x0A | Call a resource or the target device |
| **Write Bucket** | 0x0B | Write data to the target bucket |
| **Read Device Property** | 0x0C | Read the value of a device property |
| **Set Device Property** | 0x0D | Set the value of a device property |

