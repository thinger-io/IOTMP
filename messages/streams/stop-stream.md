---
description: Stops a long-lived stream previously started
---

# Stop Stream

## Request

A stop stream request is usually sent by the server to stop receiving data from a connected client, i.e., when an existing stream has been closed.

### Header

| Field            | Value                                 | Description              |
| ---------------- | ------------------------------------- | ------------------------ |
| **Message Type** | 0x09                                  | Start Stream             |
| **Message Size** | [varint](../../definitions.md#varint) | Remaining Message Length |

### Body

| Field          | Identifier | Type                                  | Mandatory | Value                      |
| -------------- | ---------- | ------------------------------------- | --------- | -------------------------- |
| **Stream Id**  | 0x01       | [varint](../../definitions.md#varint) | Yes       | Stream identifier to stop. |
| **Parameters** | 0x02       | [any](../../definitions.md#any)       | No        |                            |
| **Payload**    | 0x03       | [any](../../definitions.md#any)       | No        |                            |



## Response

| Message                          | Description                                                          |
| -------------------------------- | -------------------------------------------------------------------- |
| ****[**Ok**](../ok.md)****       | Should answer with an OK if it is able to stop the requested stream. |
| ****[**Error**](../error.md)**** | Should answer with an error if the target stream is not enabled.     |
