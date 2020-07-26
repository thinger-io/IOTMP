---
description: Message to run a resource in a device or in the broker
---

# Run

An Error Message can be sent both by clients or servers to indicate errors on a request. 

## Header

| Field | Value | Description |
| :--- | :--- | :--- |
| Message Type | 0x04 | Run |
| Message Size | varint | Remaining Message Length |

## Body

| Field | Identifier | Type | Value |
| :--- | :--- | :--- | :--- |
| Stream Id | 0x01 | varint | Stream identifier to be used in the request. Can be omitted if it is not required a confirmation. |
| **Resource**  | 0x02 |  | A string or array of strings with the resource identifier, i.e., "temperature". |
| Payload | 0x03 |  | The payload to sent to the target resource. Can be omitted if the target resource does not require a payload. |
| Action | 0x04 | varint | Represent the action to be executed: i.e., run a device resource. If not specified.  |

## Example



