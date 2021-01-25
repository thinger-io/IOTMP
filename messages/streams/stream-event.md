---
description: Message used to represent information transmitted over a stream.
---

# Stream Data

## Message

~~A `Stream Data` message represents an event sample of a resource. For example, if a server request a client resource, i.e., "temperature" without specifying interval, the client should send a `Stream Event` when considered by device, i.e, a periodical interval defined by its own, when the value changes significantly, an event is detected, and so on.~~

### Header

| Field | Value | Description |
| :--- | :--- | :--- |
| **Message Type** | 0x0A | Stream Data |
| **Message Size** | [varint](../../definitions.md#varint) | Remaining Message Length |

### Body

| Field | Identifier | Type | Mandatory | Value |
| :--- | :--- | :--- | :--- | :--- |
| **Stream Id** | 0x01 | [varint](../../definitions.md#varint) | Yes | Stream identifier. |
| **Parameters** | 0x02 | [any](../../definitions.md#any) | No | User-defined parameters associated to the information that can be used for signaling the payload, provide a context, etc. |
| **Payload** | 0x03 | [any](../../definitions.md#any) | No | Current stream payload. |

## Thinger.io

In thinger.io, clients streaming resources establish the following parameters to help the server identifying the source of information when sending 

### Parameters

| Name | Value | Description |
| :--- | :--- | :--- |
| **Resource Input** | 0x01 | Stream data represents the `current` input of the stream resource. |
| **Resource Output** | 0x02 | Stream data represents the `current` output of the stream resource. |
| **Sampling Input** | 0x03 | Stream data represents the `sampled` input of the stream resource. |
| **Sampling Output** | 0x04 | Stream data represents the `sampled` output of the stream resource. |
|  |  |  |

This help the server to determine if the information coming from a resource stream, comes from an scheduled sampling, or it has been generated as a control response. Example: One client over ws requesting by stream interval, and other by events. 

