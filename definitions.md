# Definitions

## Varint

To understand IOTMP, you first need to understand _varints_. Varints are a method of serializing integers using one or more bytes. Smaller numbers take a smaller number of bytes.

Each byte in a varint, except the last byte, has the _most significant bit_ \(msb\) set – this indicates that there are further bytes to come. The lower 7 bits of each byte are used to store the two's complement representation of the number in groups of 7 bits, **least significant group first**.

So, for example, here is the number 1 – it's a single byte, so the msb is not set:

```text
0000 0001
```

And here is 300 – this is a bit more complicated:

```text
1010 1100 0000 0010
```

How do you figure out that this is 300? First you drop the msb from each byte, as this is just there to tell us whether we've reached the end of the number \(as you can see, it's set in the first byte as there is more than one byte in the varint\):

```text
 1010 1100 0000 0010
→ 010 1100  000 0010
```

You reverse the two groups of 7 bits because, as you remember, varints store numbers with the least significant group first. Then you concatenate them to get your final value:

```text
000 0010  010 1100
→  000 0010 ++ 010 1100
→  100101100
→  256 + 32 + 8 + 4 = 300
```

## PSON

Protoson \([PSON](https://github.com/thinger-io/Protoson)\) is a method for encoding and decoding unstructured data in a binary format designed by [Thinger.io](https://thinger.io) specially for the IOT. Similar to JSON but fast and small. PSON is based on the Protocol Buffers encoding techniques, so it can achieve very small payloads over the wire, simplifying also the parsing and encoding processes. The [reference library](https://github.com/thinger-io/Protoson) done in C++ was designed with the following goals:

* **Small compiled code size**. The library has mainly designed for microcontrollers or devices with very limited resources. The whole library with encoding and decoding support takes less than 3.5KB on an Arduino. It does not require the Standard Template Library \(STL\).
* **Custom memory allocators**. Protoson C++ can use different memory allocations approaches. Currently there are implemented a circular, and a dynamic memory allocator.
* **Small output**. The output size is comparable to the well-known [MessagePack](http://msgpack.org/). Depending on the encoded data it can be even smaller.

PSON is the perfect fit for IOTMP as it shares the same encoding techniques used in [varints](definitions.md#varint), or [field keys](message-structure/message-body.md#field-key) used on the IOTMP protocol, so it can minimize the overall firmware size. However, IOTMP does not restrict the encoding techniques, so clients can use any other standard library like CBOR, or MessagePack.

## Stream

A "stream" is an independent, bidirectional sequence of messages exchanged between the client and server within an IOTMP connection. Streams have several important characteristics:

* A single IOTMQ connection can contain multiple concurrently open streams, with either endpoint interleaving frames from multiple streams.
* Streams can be established and used unilaterally or shared by either the client or server.
* Streams can be closed by either endpoint, or closed automatically depending on the message type.
* The order in which frames are sent on a stream is significant. Recipients process frames in the order they are received.
* Streams are identified by an integer. Stream identifiers are assigned to streams by the endpoint initiating the stream.

## Resources





### 



