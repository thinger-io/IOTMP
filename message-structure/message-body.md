---
description: This section describes the body encoding inside IOTMP.
---

# Message Body

Each IOTMP message body is basically a series of key-value pairs. When a message is encoded, the keys and values are concatenated into a byte stream. When the message is decoded, the parser needs to be able to skip fields that it doesn't recognize. This way, new fields can be added to a message without breaking old programs that do not know about them. To this end, the "key" for each pair in a wire-format message is actually two values – the field number according to each message definition, plus a _wire type_ that provides just enough information to find the length of the following value. In most language implementations this key is referred to as a tag.

So, the message body is composed of a variable number of fields, each one with a key-value pair:

| Field | Type | Description |
| :--- | :--- | :--- |
| **Key** | [varint](../definitions.md#varint) | Specifies the field identifier and the value type. |
| **Value** |  | The field value uses to contain integers or documents formated with JSON or other binary representations. |

## Field Key

Each key in the message is a varint that encondes both the field identifier, and the field type. The field type is called the wire type, and specifies how the value is encoded over the wire. The field identifier represents just the field for each specific message.

```text
[1-bit] [3-bit with wire type] [4-bit field identifier]
```

The following wire types are supported inside IOTMP: 

### Wire Type

| Type | Value | Used For |
| :--- | :--- | :--- |
| Varint | 0x00 | int32, int64, uint32, uint64, sint32, sint64, bool, enum |
| Fixed 64 | 0x01 | fixed64, sfixed64, double |
| Length-Delimited | 0x02 | string, bytes, embedded custom data other than PSON, i.e., CBOR, MessagePack, etc. |
| Fixed 32 | 0x05 | Specifies that the value is fixed 32 bits |
| PSON | 0x06 | Indicates that the value is encoded with PSON format |

### Field Identifier

The field identifier depends on each message, and can represent values like credentials, resource identifier, payloads, etc. So, each message specifies their own message identifiers, as described [here](../messages/).

## Field Value

Each field with a key has an associated value that can be encoded in different formats.

### Varint

A varint value is a variable integer, as defined [here](../definitions.md#varint).

### Fixed 64

A fixed 64 value is a field with fixed 64 bits \(8 bytes\).

### Length delimited

A length-delimited field contains a varint that specifies the number of bytes of the value, and the corresponding sequence of bytes. This field type is used for values with different encoders like MessagePack, UBJSON, CBOR, JSON, or any other encoding mechanishm that wants to be used.

```text
[varint with payload size][payload with specified length]
```

### Fixed 32

A fixed 32 value is a field with fixed 32 bits \(4 bytes\).

```text
[byte1 byte2 byte3 byte4]
```

### PSON

TODO

## Predefined fields

There are some common reserved field identifiers that can apply to several messages.

| Field | Field Identifier | Wire Type | Description |
| :--- | :--- | :--- | :--- |
| Reserved | 0x00 | N/A | Reserved field identifier |
| Stream Identifier | 0x01 | varint | uint16 with the stream identifier |
| Resource Identifier | 0x02 | PSON or length-delimited | Identifies a resource, it is encoded as string or array of strings |
| Payload | 0x03 | PSON or length-delimited | Represents the message payload encoded in the agreed encoding method |

### Stream Identifier

Streams are identified with an unsigned 16-bit integer. These identifiers are used basically to "map" requests with responses. 

The stream identifier is represented over the wire as follows:

```text
hexa:   0x01
binary: 0             000             0001
desc:   varint-msb    varint-type     field
```

### Resource Identifier

A resource identifier, represents, depending on the message type, a remote resource defined in the device. 

The resource identifier is represented over the wire as follows:

```text
hexa:   0x02
binary: 0             110             0001
desc:   varint-msb    pson-type       field
```

### Payload

The message paylaod contains associated data to the request, i.e., like body associated to an HTTP request.

```text
hexa:   0x23
binary: 0             010               0011
desc:   varint-msb    length-delimited  payload field
```

```text
hexa:   0x63
binary: 0             110               0011
desc:   varint-msb    pson-type         payload field
```

