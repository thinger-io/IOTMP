---
description: Stops a long-live stream previously started
---

# Stop Stream

## Request

A stop stream request is usually sent by the server to stop receiving data from a connected client, i.e., when an existing stream has been closed.

### Header

| Field | Value | Description |
| :--- | :--- | :--- |
| **Message Type** | 0x06 | Start Stream |
| **Message Size** | varint | Remaining Message Length |

### Body

| Field | Identifier | Type | Mandatory | Value |
| :--- | :--- | :--- | :--- | :--- |
| **Stream Id** | 0x01 | varint | Yes | Stream identifier to stop. |

### Example 

TBD

## Response

| Message | Description |
| :--- | :--- |
| \*\*\*\*[**Ok**](../ok.md)\*\*\*\* | Should answer with an OK if it is able to stop the requested resource at the specified interval. It must contain the Stream Id specified in this message. |
| \*\*\*\*[**Error**](../error.md)\*\*\*\* | Should answer with an Error if the target resource is not enabled or does not exists. It must contain the Stream Id specified in this message. |

