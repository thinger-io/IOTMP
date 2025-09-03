---
description: IOTMP Message Structure
---

# Message Structure

IOTMP communication is based on the exchange of structured messages between clients and servers. Each IOT **message** is composed of two main parts:

1. **Header** – mandatory, contains metadata about the message type and the size of its payload.
2. **Body (Payload)** – optional, contains the actual data being transmitted.

The general structure is:

|                          Message Structure                         |
| :----------------------------------------------------------------: |
| [Message Header](message-header.md), present in all IOTMP messages |
|   [Message Body](message-body.md), present in some IOTMP messages  |



