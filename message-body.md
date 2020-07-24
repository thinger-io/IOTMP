---
description: This section describes the body encoding inside IOTMP
---

# Message Body

The body is composed on a variable number of fields. Each field is encoded as a key-value pair, where the key field specifies the value type and the field identifier. The value 



| Field | Type | Description |
| :--- | :--- | :--- |
| Key | Varint | Specifies the field identifier and the value type. |
| Value |  |  |

## Field Encoding

Each body field requires a field identifier that is encoded using the Varint type. 

\[1-bit\]\[3-bit wire type\]\[4-bit field\]

### Wire Type

| Value | Description |
| :--- | :--- |
|  |  |



