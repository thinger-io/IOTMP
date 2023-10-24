---
description: Stops a long-lived stream previously started
---

# Stop Stream

## Request

A stop stream request is usually sent by the server to stop receiving data from a connected client, i.e., when an existing stream has been closed.

### Header

<table><thead><tr><th width="186.33333333333331">Field</th><th width="105">Value</th><th>Description</th></tr></thead><tbody><tr><td><strong>Message Type</strong></td><td>0x09</td><td>Start Stream</td></tr><tr><td><strong>Message Size</strong></td><td><a href="../../definitions.md#varint">varint</a></td><td>Remaining Message Length</td></tr></tbody></table>

### Body

<table><thead><tr><th width="153">Field</th><th width="112">Identifier</th><th width="109">Type</th><th width="120">Mandatory</th><th>Value</th></tr></thead><tbody><tr><td><strong>Stream Id</strong></td><td>0x01</td><td><a href="../../definitions.md#varint">varint</a></td><td>Yes</td><td>Stream identifier to stop.</td></tr><tr><td><strong>Parameters</strong></td><td>0x02</td><td><a href="../../definitions.md#any">any</a></td><td>No</td><td></td></tr><tr><td><strong>Payload</strong></td><td>0x03</td><td><a href="../../definitions.md#any">any</a></td><td>No</td><td></td></tr></tbody></table>



## Response

| Message                  | Description                                                          |
| ------------------------ | -------------------------------------------------------------------- |
| [**Ok**](../ok.md)       | Should answer with an OK if it is able to stop the requested stream. |
| [**Error**](../error.md) | Should answer with an error if the target stream is not enabled.     |
