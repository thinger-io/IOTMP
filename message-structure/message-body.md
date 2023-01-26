---
description: IOTMP Message Body
---

# Message Body

The message **body**, also known as the payload, is the portion of a message that contains the actual data being transmitted. It follows the header and contains the information that the sender intends to send to the receiver.

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

The wire type specifies the format used for encoding each data field. IOTMP relies on [JSON](https://www.json.org/) format or its derivates, so, different JSON encoding formats can be supported on an IOTMP server, i.e., JSON, PSON, MessagePack, CBOR, etc. This way, different client implementations can choose the preferred encoding format, according to their needs, library availability, etc. The default encoding formats that an IOTMP server MUST support are [PSON](https://www.mdpi.com/1424-8220/21/13/4559), and JSON.

An IOTMP client MUST support at least one of the default formats: PSON or JSON. It is always preferred PSON encoding, as it can improve the overall performance by reducing serialization and deserialization complexity, and reduces bandwidth with a more compact representation. JSON encoding can be used by convenience, i.e., when running IOTMP inside a browser.

By default, IOTMP specifies 4 different wire types:

* **Varint (0x00)**: Indicates that the value holds an integer encoded as [varint](../definitions.md#varint).
* **PSON (0x01)**: Indicates that the value holds a JSON encoded with PSON.
* **JSON (0x02)**: Indicates that the value holds a JSON without any binary encoding.
* **Negotiated (0x07)**: Indicates that the value holds a JSON encoded with a negotiated binary representation, i.e., MessagePack, CBOR, UBJSON.

| Type           | Value                       | Used For                                                                                                                                                                                                                |
| -------------- | --------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Varint**     | 0x00                        | Positive number encoded as [varint](../definitions.md#varint). It is heavily used in the protocol for specifying fields like the stream identifier.                                                                     |
| **PSON**       | 0x01                        | Value is encoded in PSON format. As PSON supports streaming decoding, the payload is encoded right away after the key.                                                                                                  |
| **JSON**       | 0x02                        | Value is encoded in JSON format. The value is composed by a [varint](../definitions.md) (specifying total payload size) + the custom JSON payload.                                                                      |
| **Reserved**   | <p>0x03  </p><p>to 0x06</p> | Reserved for future usage.                                                                                                                                                                                              |
| **Negotiated** | 0x07                        | Value is encoded in the negotiated encoding format (see [Connect Message](../messages/connect.md)). The value is composed by a [varint](../definitions.md) (specifying total value size) + the custom encoded payload.  |

{% hint style="info" %}
It is preferred to use PSON encoding format when possible, as it reduces encoding/decoding complexity, and reduces overall bandwidth.
{% endhint %}

### Field Identifier

The field identifier depends on each message, so, each one specifies their own message identifiers, as described [here](../messages/).

## Value

Each field with a key has an associated value that can be encoded in different formats, according to the specification provided on the [Wire-Type](message-body.md#wire-type).

