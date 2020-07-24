---
description: This section describes the body encoding inside IOTMP
---

# Message Body

The body is composed on a variable number of fields. Each field is encoded as a key-value pair, where the key field specifies the value type and the field identifier. The value 



| Field | Type | Description |
| :--- | :--- | :--- |
| Key | Varint | Specifies the field identifier and the value type. |
| Value | Variable | The field value uses to contain integers or documents formated with JSON or other binary representations. |

## Field Identifier

Each body field requires a field identifier that is encoded using the Varint type. The field identifier

\[1-bit\]\[3-bit wire type\]\[4-bit field\]

### Wire Type

| Type | Value | Description |
| :--- | :--- | :--- |
| Varint | 0x00 | Specifies that the value is a Varint |
| Fixed 64 | 0x01 | Specifies that the value is fixed 64 bits |
| Length Delimited | 0x02 | Specifies that the value is length-delimited |
| Message Pack | 0x03 | Specifies that the value is using MessagePack encoding |
| UBJSON | 0x04 | Specifies that the value is using UBJSON encoding |
| Fixed 32 | 0x05 | Specifies that the value is fixed 32 bits |
| PSON | 0x06 | Specifies that the value is using PSON encoding |
| JSON | 0X07 | Specifies that the value is using JSON encoding |
| CBOR | 0x08 | Specifies that the value is using CBOR encoding |

#### Varint

#### Fixed 64

#### Lenght delimited

#### Message Pack

#### UBJSON

#### Fixed 32

#### PSON

#### JSON

#### CBOR

## Field Value

