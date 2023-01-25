---
description: This section describes the body encoding inside IOTMP.
---

# Message Body

## Key-Value Pairs

Each IOTMP message consists basically on a series of `key-value` pairs. When a message is encoded, the keys and values are concatenated into a byte stream. When the message is decoded, the parser needs to be able to skip fields that it doesn't recognize. This way, new fields can be added to a message without breaking old programs that do not know about them. To this end, the "key" for each pair in a wire-format message is actually two values – the field number according to each message definition, plus a [Wire-Type](message-body.md#wire-type), that provides just enough information to find the length of the following value.

So, the message body is composed of a variable number of fields, each one with a key-value pair:

| Field                                      | Type                               | Description                                        |
| ------------------------------------------ | ---------------------------------- | -------------------------------------------------- |
| ****[**Key**](message-body.md#key)****     | [varint](../definitions.md#varint) | Specifies the field identifier and the value type. |
| ****[**Value**](message-body.md#value)**** | [any](../definitions.md#any)       | Contains the actual payload of the field.          |

## Key

Each key in the message is a [varint](../definitions.md#varint) that encodes both the **Field Identifier**, and the **Wire type**.&#x20;

A **Field Identifier** represents just the field for each specific message, i.e., if the value is related with a stream identifier, a parameter, or a payload.

The **Wire Type** specifies how the value is encoded over the wire, as each body value can be encoded in different formats depending on the client and server implementation.

Then, a **Key** (with both Field Identifier and Wire Type) is encoded as a [varint](../definitions.md#varint), where the first 3 bits indicates the [Wire-Type](message-body.md#wire-type), and the 4 remaining bits indicates the [Field Identifier](../definitions.md#field-identifier). This schema is described below:

```
[1-bit][4-bit field identifier][3-bit with wire type] 
```

For example, a key with a wire-type (0) and a field identifier (1) would be encoded as the following:

```
[0][0001][000] 
```

It is possible to use a [varint](../definitions.md#varint) of two or more bytes in order to extend the field identifier. But in general terms, one byte covers up to 2^4 (16) Field Identifiers, and up to 2^3 (8) Wire Types, that should be enough for most use-cases.

The following wire types are supported by default inside IOTMP:&#x20;

### Wire Type

The wire type specifies the format used for encoding each data field. IOTMP relies on JSON format or its derivates, so, different JSON encoding formats can be supported on an IOTMP server, i.e., PSON, MessagePack, CBOR, etc., so, different client implementations can choose the preferred encoding format, according to their needs, library availability, etc. It is preferred JSON binary representations, like [PSON](https://github.com/thinger-io/Protoson) or [MessagePack](https://msgpack.org/), as they can be used to send binary data, which can be required by some services provided over IOTMP.

By default, IOTMP supports 3 wire types:

* **Varint**: Indicates that the value holds an integer encoded as varint.
* **Self-contained**: Indicates that the value holds a binary representation that is self-contained, and can be decoded without additional information like total buffer size.
* **Length-Delimited**: Indicates that the field holds an arbitrary data representation that may require to know the total buffer size before its decoding.

| Type                 | Value       | Used For                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| -------------------- | ----------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Varint**           | 0x00        | Positive number encoded as [varint](../definitions.md#varint). It is heavily used in the protocol for specifying fields like the stream identifier.                                                                                                                                                                                                                                                                                                                                                                                |
| **Self-Contained**   | 0x01        | <p>Used for binary data that can be decoded without reading the entire data block before starting its decoding, i.e., the encoding and the library implementation supports stream decoding as the data is read being read from a socket.</p><p></p><p>A library implementation supporting binary JSON with stream decoding is <a href="https://github.com/thinger-io/Protoson">PSON</a>.</p>                                                                                                                                       |
| **Length-Delimited** | 0x02        | <p>Used for other representations or library implementations that does not support data decoding in streaming, i.e., requires to know the buffer size and have a complete message representation for its decoding. </p><p></p><p>In such cases, the value is composed by a <a href="../definitions.md">varint</a>  (specifying total field size) + the custom buffer.  For example, a plain JSON representation or a library that does not support stream decoding will require to know the total buffer size before decoding.</p> |
| **Reserved**         | 0x03 - 0x07 | Reserved for future use.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |

{% hint style="info" %}
It is preferred to use self-contained encoding when possible, as it can save some bandwidth on each field.
{% endhint %}

### Field Identifier

The field identifier depends on each message, so, each one specifies their own message identifiers, as described [here](../messages/).

## Value

Each field with a key has an associated value that can be encoded in different formats, according to the specification provided on the [Wire-Type](message-body.md#wire-type).

