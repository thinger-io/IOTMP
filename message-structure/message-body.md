---
description: This section describes the body encoding inside IOTMP.
---

# Message Body

Each IOTMP message body is basically a series of `key-value` pairs. When a message is encoded, the keys and values are concatenated into a byte stream. When the message is decoded, the parser needs to be able to skip fields that it doesn't recognize. This way, new fields can be added to a message without breaking old programs that do not know about them. To this end, the "key" for each pair in a wire-format message is actually two values – the field number according to each message definition, plus a _wire type_ that provides just enough information to find the length of the following value. In most language implementations this key is referred to as a tag.

So, the message body is composed of a variable number of fields, each one with a key-value pair:

| Field | Type | Description |
| :--- | :--- | :--- |
| **Key** | [varint](../definitions.md#varint) | Specifies the field identifier and the value type. |
| **Value** | value | The field value uses to contain integers or documents formatted with JSON or other binary representations. |

## Pair Key

Each key in the message is a varint that encodes both the key identifier, and the value type. The value type is called the wire type, and specifies how the value is encoded over the wire. The key identifier represents just the field for each specific message, i.e., if the value is related with a paylaod, a stream identifier, a response code, etc.

```text
[1-bit][4-bit field identifier][3-bit with wire type] 
```

The following wire types are supported inside IOTMP: 

### Wire Type

| Type | Value | Used For |
| :--- | :--- | :--- |
| Varint | 0x00 | int32, int64, uint32, uint64, sint32, sint64, bool, enum |
| PSON | 0x01 | Values in [PSON ](https://github.com/thinger-io/Protoson)format |
| JSON | 0x02 | Values in [JSON ](https://www.json.org)format |
| MESSAGEPACK | 0x03 | Values in [MessagePack ](https://msgpack.org/)format |
| BSON | 0x04 | Values in [BSON ](http://bsonspec.org/)format |
| CBOR | 0x05 | Values in [CBOR ](https://cbor.io/)format |
| UBJSON | 0x06 | Values in [UBJSON ](https://ubjson.org/)format |

### Field Identifier

The field identifier depends on each message, and can represent values like credentials, resource identifier, payloads, etc. So, each message specifies their own message identifiers, as described [here](../messages/).

## Pair Value

Each field with a key has an associated value that can be encoded in different formats.

### Varint

A `varint` value is a variable size integer, as defined [here](../definitions.md#varint).

### PSON

### JSON

### MessagePack

### BSON

### CBOR

### UBJSON

