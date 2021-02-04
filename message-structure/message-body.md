---
description: This section describes the body encoding inside IOTMP.
---

# Message Body

## Key-Value Pairs

Each IOTMP message consists basically on a series of `key-value` pairs. When a message is encoded, the keys and values are concatenated into a byte stream. When the message is decoded, the parser needs to be able to skip fields that it doesn't recognize. This way, new fields can be added to a message without breaking old programs that do not know about them. To this end, the "key" for each pair in a wire-format message is actually two values – the field number according to each message definition, plus a _wire type_ that provides just enough information to find the length of the following value.

So, the message body is composed of a variable number of fields, each one with a key-value pair:

| Field | Type | Description |
| :--- | :--- | :--- |
| **Key** | [varint](../definitions.md#varint) | Specifies the field identifier and the value type. |
| **Value** | [any](../definitions.md#any) | Contains the actual payload of the field. |

## Key

Each key in the message is a [varint](../definitions.md#varint) that encodes both the key identifier, and the value type. The value type is called the wire type, and specifies how the value is encoded over the wire. The key identifier represents just the field for each specific message, i.e., if the value is related with a stream identifier, a payload, a parameter, etc.

The key is then a [varint](../definitions.md#varint), where the first 3 bits indicates the [Wire-Type](message-body.md#wire-type), and the 4 remaining bits indicates the [Field Identifier](../definitions.md#field-identifier). This schema is described below:

```text
[1-bit][4-bit field identifier][3-bit with wire type] 
```

For example, a key with a wire-type \(0\) and a field identifier \(1\) would be encoded as the following:

```text
[0][0001][000] 
```

The following wire types are supported by default inside IOTMP: 

### Wire Type

| Type | Value | Used For |
| :--- | :--- | :--- |
| **Varint** | 0x00 | Positive number encoded as [Varint](../definitions.md#varint)  |
| **Signed Varint** | 0x01 | Negative number encoded as [Varint](../definitions.md#varint) |
| **Float** | 0x02 | \(32 bits\) IEEE 754 Single-precision floating-point |
| **Double** | 0x03 | \(64 bits\) IEEE 754 Double-precision floating-point |
| **String** | 0x04 | Length delimited string: [Varint](../definitions.md) \(specifying size\) + Buffer |
| **Bytes** | 0x05 | Length delimited bytes: Varint \(specifying size\) + Buffer |
| **Negotiated Encoding** | 0x06 | Length delimited bytes: Varint \(specifying size\) + Buffer |

### Field Identifier

The field identifier depends on each message, so, each one specifies their own message identifiers, as described [here](../messages/).

## Value

Each field with a key has an associated value that can be encoded in different formats, according to the specification provided on the [Wire-Type](message-body.md#wire-type).

### Varint

### Signed Varint

### Float

### Double

### String

### Bytes

### Negotiated Encoding



