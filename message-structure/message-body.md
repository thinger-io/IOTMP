---
description: IOTMP Message Body
---

# Message Body

The message **body**, also known as the payload, is the portion of a message that contains the actual data being transmitted. It follows the header and contains the information that the sender intends to send to the receiver.

## Key-Value Pairs

Each IOTMP message consists basically on a series of `key-value` pairs. When a message is encoded, the keys and values are concatenated into a byte stream. When the message is decoded, the parser needs to be able to skip fields that it doesn't recognize. This way, new fields can be added to a message without breaking old programs that do not know about them. To this end, the "key" for each pair in a wire-format message is actually two values – the field number according to each message definition, plus a [Wire-Type](message-body.md#wire-type), that provides just enough information to find the length of the following value.

So, the message body is composed of a variable number of fields, each one with a key-value pair:

<table><thead><tr><th width="96.33333333333331">Field</th><th width="76">Type</th><th>Description</th></tr></thead><tbody><tr><td><a href="message-body.md#key"><strong>Key</strong></a></td><td><a href="../definitions.md#varint">varint</a></td><td>Specifies the field identifier and the value type.</td></tr><tr><td><a href="message-body.md#value"><strong>Value</strong></a></td><td><a href="../definitions.md#any">any</a></td><td>Contains the actual payload of the field.</td></tr></tbody></table>

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

The IOTMP protocol currently supports two primary wire types, Varint and [PSON](https://www.mdpi.com/1424-8220/21/13/4559), which are designed to efficiently encode data. The Varint type is optimized for storing positive integers, used mainly on protocol identifiers, while the PSON type is intended for encoding data structures in a more complex format. This approach allows for adaptable data transmission across various devices in IoT ecosystems.

<table><thead><tr><th width="185.33333333333331">Type</th><th width="103.41796875">Value</th><th>Used For</th></tr></thead><tbody><tr><td><strong>Varint</strong></td><td>0x00</td><td>Positive number encoded as <a href="../definitions.md#varint">varint</a>. It is heavily used in the protocol for specifying fields like the stream identifier.</td></tr><tr><td><strong>PSON</strong></td><td>0x01</td><td>Value is encoded in <a href="https://www.mdpi.com/1424-8220/21/13/4559">PSON</a> format. As PSON supports streaming decoding, the payload is encoded right away after the key.</td></tr><tr><td>Reserved</td><td>0x02 - 0x06</td><td>Reserved for future use</td></tr></tbody></table>

### Field Identifier

The field identifier depends on each message, so, each one specifies their own message identifiers, as described [here](../messages/).

## Value

Each field with a key has an associated value that can be encoded in different formats, according to the specification provided on the [Wire-Type](message-body.md#wire-type).

