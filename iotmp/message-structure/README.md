# Message Structure

The IOTMP protocol works by exchanging a series of IOTMP messages in a defined way. This section describes the format of these packets.

Each IOTMP message contains a **header** and an optional **body:**

* The **header** is a part of a message that contains information about the type of message and the size of the data being transmitted.
* The message **body**, also known as the payload, is the portion of a message that contains the actual data being transmitted. It follows the header and contains the information that the sender intends to send to the receiver. The size of the message body is specified in the header and can be used to determine the total size of the packet.

|               Message Structure               |
| :-------------------------------------------: |
| Message Header, present in all IOTMP messages |
|  Message Body, present in some IOTMP messages |



