---
description: Message used to represent an event sample in an opened stream
---

# Stream Event

## Message

A `Stream Event` message represents an event sample of a resource. For example, if a server request a client resource, i.e., "temperature" without specifying interval, the client should send a `Stream Event` when considered by device, i.e, a periodical interval defined by its own, when the value changes significantly, an event is detected, and so on.

### Header

| Field | Value | Description |
| :--- | :--- | :--- |
| **Message Type** | 0x0B | Stream Sample |
| **Message Size** | [varint](../../definitions.md#varint) | Remaining Message Length |

### Body

| Field | Identifier | Type | Mandatory | Value |
| :--- | :--- | :--- | :--- | :--- |
| **Stream Id** | 0x01 | [varint](../../definitions.md#varint) | Yes | Stream identifier. |
| **Context** | 0x02 | [varint](../../definitions.md#varint) | No | Flag that allows identifying the source of a stream event. It can help routing the information in the server. |
| **Payload** | 0x03 |  | No | Current event payload |
| Parameters | 0x04 |  | No | Ad |

### Context

| Field | Value | Description |
| :--- | :--- | :--- |
| **Device Resource Input** | 0x01 | The stream payload is associated to a resource input, i.e., a switch state, config parameters, etc. ~~TBC: Echo~~ |
| **Device Resource Output** | 0x02 | The stream payload is associated to a resource output \(data generated inside a resource, i.e., a sensor reading\). |
| **Device Resource Sample** | 0x03 | The stream payload is associated to a scheduled resource sample, i.e., a message sent every 5 seconds as requested in a [Start Stream](start-stream.md). |
| **Device Resource Stream** | 0x04 | The stream payload is associated to a stream over a device resource. |
| **Topic Stream** | 0x05 | The information has been generated to publish on  |
|  |  |  |

