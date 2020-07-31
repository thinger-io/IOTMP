---
description: Message to run a resource in a device or in the broker.
---

# Run Resource

This message enables running remote [resources ](../definitions.md#resources)defined both in client and server. Resources are defined dynamically by clients and servers. As described in the [resources ](../definitions.md#resources)definition, a resource is basically like a function that can be executed like in RPC \(Remote Procedure Call\). As a "function" it can receive inputs, and provide an output. 

A **device** can define multiple resources as required by its use case, i.e., read humidity, adjust temperature, turn on a light, etc.  Typical resources for an IoT device are functions for reading device states, sensor values, adjust parameters, or actuating over digital pins to mention a few.

A **server** or broker can also define multiple resources that can be executed by their clients. Such resources can vary depending on the use case, and normally involves complex task that are not worth to be executed in the device. Typical resources defined by a server can be actions like writing to a database, calling an external endpoint for sending communications, managing device configuration, etc.

## Request

### Header

| Field | Value | Description |
| :--- | :--- | :--- |
| **Message Type** | 0x06 | Run |
| **Message Size** | [varint](../definitions.md#varint) | Remaining Message Length |

### Body

| Field | Identifier | Type | Mandatory | Value |
| :--- | :--- | :--- | :--- | :--- |
| **Stream Id** | 0x01 | [varint](../definitions.md#varint) | No | [Stream identifier](../definitions.md#stream-identifier). |
| **Resource**  | 0x02 |  | Yes | [Resource identifier](../definitions.md#resource-identifier). |
| **Payload** | 0x03 |  | No | The payload sent to the target resource. Can be omitted if the target resource does not require an input. |
| **Parameters** | 0x04 |  | No | [Resource parameters](../definitions.md#resource-parameters) to be supplied while executing  the resource. |

## Responses

### OK

The resource executed correctly.

| Field | Identifier | Type | Mandatory | Value |
| :--- | :--- | :--- | :--- | :--- |
| **Stream Id**  | 0x01 | [varint](../definitions.md#varint) | Yes | [Resource identifier](../definitions.md#resource-identifier) associated to the request. |
| **Payload** | 0x03 |  | No | The response payload that generated in the resource execution. |

### Error

An error occurred while executing the resource..

| Field | Identifier | Type | Mandatory | Value |
| :--- | :--- | :--- | :--- | :--- |
| **Stream Id**  | 0x01 | [varint](../definitions.md#varint) | Yes | [Resource identifier](../definitions.md#resource-identifier) associated to the request. |
| **Payload** | 0x03 |  | No | Additional error information. |

