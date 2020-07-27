---
description: Message used to cleanly disconnect a current connection.
---

# Disconnect

## Request

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
| **Payload** | 0x03 |  | Yes | Authentication payload as defined by the `Auth Type` field. By default, the `Auth Type` is 1 \(credentials\), so the `Payload` MUST contain an array with the username, device identifier, and credentials.  |
| **Auth Type** | 0x04 | varint | No | Depending on the value, the authentication is done over different mechanisms, like credentials, certificates, token, etc. |
| **Keep Alive** | 0x05 | varint | No | Establish a Keep Alive interval in seconds \(60 seconds by default\). |



