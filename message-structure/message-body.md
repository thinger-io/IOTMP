---
description: IOTMP Message Body
---

# Message Body

The **message body** (payload) contains the actual data transmitted between client and server. It directly follows the header and its size is defined by the **Message Size** field.

The body is composed of a sequence of **key–value pairs**, which provide a flexible and extensible way to encode data.

### Key–Value Pairs

Each message body consists of zero or more **key–value pairs**, concatenated into a byte stream.

* **Keys** identify the field and how its value is encoded.
* **Values** hold the actual data.
* Parsers must be able to **skip unrecognized keys**, ensuring forward compatibility: new fields can be added without breaking older implementations.

<table><thead><tr><th width="96.33333333333331">Field</th><th width="76">Type</th><th>Description</th></tr></thead><tbody><tr><td><a href="message-body.md#key"><strong>Key</strong></a></td><td><a href="../definitions.md#varint">varint</a></td><td>Encodes both the field identifier and the wire type.</td></tr><tr><td><a href="message-body.md#value"><strong>Value</strong></a></td><td><a href="../definitions.md#any">any</a></td><td>Contains the actual payload of the field.</td></tr></tbody></table>

### Key

A **Key** is encoded as a **varint** that combines two elements:

1. **Field Identifier** – specifies the meaning of the field (e.g., stream ID, parameter, payload).
2. **Wire Type** – specifies how the value is encoded on the wire.

The binary layout of a key is:

```
[continuation bit][field identifier (4 bits)][wire type (3 bits)]
```

* **4-bit Field Identifier** → up to 16 unique fields per message (extendable with multi-byte varints).
* **3-bit Wire Type** → up to 8 encoding formats.
* **Continuation bit** → allows extending the field identifier beyond 4 bits.

**Example:**\
A key with wire type `0` (Varint) and field identifier `1` is encoded as:

```
[0][0001][000]
```

This compact scheme ensures efficient encoding while allowing future extensibility.

#### Wire Type

The **Wire Type** specifies how the value associated with a key is encoded on the wire. It is encoded in the **3 least significant bits** of the key varint.

Currently, IOTMP defines the following wire types:

<table><thead><tr><th width="185.33333333333331">Type</th><th width="103.41796875">Value</th><th>Used For</th></tr></thead><tbody><tr><td><strong>Varint</strong></td><td>0x00</td><td>Positive integers encoded as varint. Commonly used for protocol identifiers (e.g., stream ID).</td></tr><tr><td><strong>PSON</strong></td><td>0x01</td><td>Structured data encoded in PSON. Supports streaming decoding, allowing the payload to be read immediately after the key.</td></tr><tr><td>Reserved</td><td>0x02 - 0x06</td><td>Reserved for future extensions.</td></tr></tbody></table>

This design allows IOTMP to support both **lightweight numeric values** (varint) and **complex data structures** (PSON), while keeping room for additional encodings in the future.

#### Field Identifier

The **Field Identifier** specifies the role of the field within a message.

* Encoded in the **4 bits** of the key (plus additional bytes if extended).
* Determines the semantic meaning of the value (e.g., stream identifier, parameter, payload).
* Each message definition specifies its own set of valid field identifiers.

This allows different message types to reuse the same encoding scheme while defining their own unique fields.

### Value

The **Value** represents the actual payload associated with a key.

* Its encoding is determined by the **Wire Type**.
* Can be a simple integer (varint) or a structured object (PSON).
* Parsers must be able to skip values they do not recognize, preserving forward compatibility.

Values are placed in the message body **immediately after their key**, enabling compact and efficient encoding.
