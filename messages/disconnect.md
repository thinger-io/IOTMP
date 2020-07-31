---
description: Message used to cleanly disconnect a current connection.
---

# Disconnect

## Message

A `Disconnect`message can be sent anytime to close an ongoing connection. It can be initiated both by the server or the client.

### Header

| Field | Value | Description |
| :--- | :--- | :--- |
| **Message Type** | 0x04 | Disconnect |
| **Message Size** | [varint](../definitions.md#varint) | Remaining Message Length |

### Body

| Field | Identifier | Type | Mandatory | Value |
| :--- | :--- | :--- | :--- | :--- |
| **Stream Id** | 0x01 | [varint](../definitions.md#varint) | No | Request Identifier. |
| **Reason** | 0x02 | [varint](../definitions.md#varint) | No | Disconnect reason. |
| **Payload** | 0x03 |  | No |  |

### Reason Values

| Value | Description |
| :--- | :--- |
| **0x01** | TBD |

