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

Protoson \(PSON\) is a method for encoding and decoding unstructured data in a binary format.

 Similar to JSON but fast and small. Protoson is based on some Protocol Buffers encoding techniques.





### 



