---
description: Message to run a resource in a device or in the broker.
---

# Run Resource

This message enables running remote [resources ](../definitions.md#resources)defined both in client and server. Resources are defined dynamically by clients and servers. As described in the [resources ](../definitions.md#resources)definition, a resource is basically like a function that can be executed like in RPC (Remote Procedure Call). As a "function" it can receive inputs, and provide an output.&#x20;

A **device** can define multiple resources as required by its use case, i.e., read humidity, adjust temperature, turn on a light, etc.  Typical resources for an IoT device are functions for reading device states, sensor values, adjust parameters, or actuating over digital pins to mention a few.

A **server** or broker can also define multiple resources that can be executed by their clients. Such resources can vary depending on the use case, and normally involves complex task that are not worth to be executed in the device. Typical resources defined by a server can be actions like writing to a database, calling an external endpoint for sending communications, managing device configuration, etc.

## Request

### Header

| Field            | Value                              | Description              |
| ---------------- | ---------------------------------- | ------------------------ |
| **Message Type** | 0x06                               | Run                      |
| **Message Size** | [varint](../definitions.md#varint) | Remaining Message Length |

### Body

<table><thead><tr><th>Name</th><th>Field</th><th data-type="select">Type</th><th data-type="checkbox">Mandatory</th><th>Description</th></tr></thead><tbody><tr><td><strong>Resource</strong> </td><td>0x00</td><td></td><td>true</td><td><a href="../definitions.md#resource-identifier">Resource identifier</a>.</td></tr><tr><td><strong>Stream Id</strong></td><td>0x01</td><td></td><td>false</td><td><a href="../definitions.md#stream-identifier">Stream identifier</a>. If set, the target endpoint should answer to the run message. If not, it should not send back any response.</td></tr><tr><td><strong>Parameters</strong></td><td>0x02</td><td></td><td>false</td><td><a href="../definitions.md#resource-parameters">Resource parameters</a> to be supplied while executing  the resource.</td></tr><tr><td><strong>Payload</strong></td><td>0x03</td><td></td><td>false</td><td>The payload sent to the target resource.</td></tr></tbody></table>

## Responses

### OK

The resource executed correctly.

### Error

An error occurred while executing the resource.
