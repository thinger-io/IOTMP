---
description: Message to run a resource in a device or in the broker
---

# Run Resource

This message enables running remote [resources ](../definitions.md#resources)defined both in client and server. Resources are defined dynamically by clients and servers. As described in the [resources ](../definitions.md#resources)definition, a resource is basically like a function that can be executed like in RPC \(Remote Procedure Call\). As a "function" it can receive inputs, and provide an output. 

A **device** can define multiple resources as required by its use case, i.e., read humidity, adjust temperature, turn on a light, etc.  Typical resources for an IoT device are functions for reading device states, sensor values, adjust parameters, or actuating over digital pins to mention a few.

A **server** or broker can also define multiple resources that can be executed by their clients. Such resources can vary depending on the use case, and normally involves complex task that are not worth to be executed in the device. Typical resources defined by a server can be actions like writing to a database, calling an external endpoint for sending communications, managing device configuration, etc.

## Request

### Header

| Field | Value | Description |
| :--- | :--- | :--- |
| **Message Type** | 0x04 | Run |
| **Message Size** | varint | Remaining Message Length |

### Body

| Field | Identifier | Type | Mandatory | Value |
| :--- | :--- | :--- | :--- | :--- |
| _**Stream Id**_ | 0x01 | varint | No | [Stream identifier](../definitions.md#stream-identifier). |
| **Resource**  | 0x02 |  |  | [Resource identifier](../definitions.md#resource-identifier). |
| _**Payload**_ | 0x03 |  |  | The payload sent to the target resource. Can be omitted if the target resource does not require a payload. |

## Response

### OK

The resource executed correctly

### Error

The resource cannot be executed, i.e, it does not exists, or there are problems with the supplied parameters

