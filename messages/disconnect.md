---
description: Message used to cleanly disconnect a current connection.
---

# Disconnect

## Message

A `Disconnect`message can be sent anytime to close an ongoing connection. It can be initiated both by the server or the client.

### Header

| Field | Value | Description |
| :--- | :--- | :--- |
| **Message Type** | 0x09 | Disconnect |
| **Message Size** | varint | Remaining Message Length |

### Body

| Field | Identifier | Type | Mandatory | Value |
| :--- | :--- | :--- | :--- | :--- |
| **Stream Id** | 0x01 | varint | Yes | Request Identifier. |
| **Reason** | 0x04 | varint | No | Disconnect reason. |



