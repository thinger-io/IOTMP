---
description: >-
  Initiates a long-live stream for transmitting periodic data associated to a
  resource.
---

# Start Stream

## Request

A start stream request is usually sent by the server to start receiving data from a connected client, i.e., when a stream is opened to consume the resource information \(a dashboard, mobile App, etc.\).

### Header

| Field | Value | Description |
| :--- | :--- | :--- |
| **Message Type** | 0x08 | Start Stream |
| **Message Size** | [varint](../../definitions.md#varint) | Remaining Message Length |

### Body

| Field | Identifier | Type | Mandatory | Value |
| :--- | :--- | :--- | :--- | :--- |
| **Stream Id** | 0x01 | [varint](../../definitions.md#varint) | Yes | Stream identifier to be used within the stream life-time. |
| **Resource**  | 0x02 |  | First Time | A string or array of strings with the resource identifier, i.e., "temperature". It is only mandatory the first time the stream is opened. Following Start Streams over the same Stream Id can be used fo reconfigure the interval, so it is not required to specify again the resource. |
| **Interval** | 0x03 | [varint](../../definitions.md#varint) | No | Sampling interval in seconds. If the field is not present or zero,  just allows the target resource to stream the resource as considered, i.e., when there is an event.  |

### Example 

TBD

## Response

| Message | Description |
| :--- | :--- |
| \*\*\*\*[**Ok**](../ok.md)\*\*\*\* | Should answer with an OK if it is able to stream the requested resource at the specified interval. It must contain the Stream Id specified in this message. |
| \*\*\*\*[**Error**](../error.md)\*\*\*\* | Should answer with an Error if the target resource cannot be streamed at the specified interval. It must contain the Stream Id specified in this message. |

### Example

TBD

## Stream Messages

| Message | Description |
| :--- | :--- |
| \*\*\*\*[**Stream Sample**](stream-sample.md)\*\*\*\* | If the resource has been configured with a sampling interval, it must send the data using the `Stream Sample` message, that represents a periodical sampling data over the stream.  |
| \*\*\*\*[**Stream Event**](stream-event.md)\*\*\*\* | If the resource has been configured without a sampling interval, it must send the data using the `Stream Event` message, that represents a message over the stream.  |
| \*\*\*\*[**Stop Stream**](stop-stream.md)\*\*\*\* | A `Stop Stream` can be sent anytime during the stream life-time to conclude the streaming. |
| \*\*\*\*[**Start Stream**](start-stream.md)\*\*\*\* | A `Start Stream` can be sent anytime by the requester to reconfigure the sampling interval. In such case, should send only the Stream Identifier and the new Interval. |

## Client Implementation notes

### Resource definition

A resource to be used in a stream should be defined in the same way to a normal resource that can be executed over the [Run ](../run.md)message, i.e., a resource defined with the [Thinger.io Arduino Library](https://github.com/thinger-io/Arduino-Library) is defined as the following:

```cpp
void setup(){
  thing["heading"] >> [](pson& out){     
    out = getHeading();
  };
}
```

Internally, the client should keep information about each resource state, i.e., the associated stream identifier \(if any\), and the latest stream timestamp.

{% hint style="info" %}
From the perspective of a developer creating a firmware, streams should be completely transparent to the resource definition.
{% endhint %}

### Streaming with a Sampling interval

When a `Start Stream` message is received with a sampling interval, the client should look for the requested resource, and then adjust the `Stream Identifier` and the expected timestamp. In each loop, it should check all the enabled streams, and then transmit those which are required according to its timestamp and sampling interval. If a following `Start Stream` is received for the same resource, it must overwrite it, that is, update its interval, or change the Stream Identifier if necessary \(depending if the message comes only with Stream Id or Stream Id and Resource\).

### Streaming Events

To send events over a stream, it is usually required to detect the event or the change. It is completely dependent on the use case, so, the firmware must be prepared to detect and transmit the information when it is required. In the following example, the same `heading` resource defined before is transmitted if it is detected an angle difference greater than one degree. To to this, the [Thinger.io Arduino Library](https://github.com/thinger-io/Arduino-Library) defines a method to stream a given resource. This method should take into account if this resource Stream is enabled, that is, it contains a `Stream Identifier`, otherwise the message must not be sent \(as there is no anyone listening for it\).

```cpp
void setup(){
  thing["heading"] >> [](pson& out){     
    out = getHeading();
  };
}

float previousHeading = 0;
void loop() {
  thing.handle();
  float currentHeading = getHeading();
  if(abs(currentHeading-previousHeading)>=1.0f){
    thing.stream("heading");
    previousHeading=currentHeading;
  }
}
```

![Example ESP8266 running IOTMP for sending heading when there is a subtle difference.](../../.gitbook/assets/image%20%283%29.png)

## Server Implementation notes

### HTTP/REST API Integration

As described before, a typical scenario where a `Start Stream` is required is when a new `Websocket`or `Server Sent Event` is opened over the server to start listening over a resource, for example, to feed a real-time dashboard. In [Thinger.io](https://Thinger.io) implementation, a device resource endpoint is defined as follow:

```text
https://.../v3/users/alvarolb/devices/smart_irrigation/resources/temp
```

In such implementation it is possible to open a `Websocket` over the resource, so the endpoint is now:

```text
wss://.../v3/users/alvarolb/devices/smart_irrigation/resources/temp
```

Opening such `Websocket` will listen for events on the `temp` resource, that is, changes that are detected by device and transmitted to the `Websocket`. But it is possible to open also the resource as following:

```text
wss://.../v3/users/alvarolb/devices/smart_irrigation/resources/temp?interval=5
```

In such case, the `Websocket` will start receiving the information every 5 seconds. Moreover, it is possible to open an endpoint without defining a resource:

```text
wss://.../v3/users/alvarolb/devices/smart_irrigation/resources
```

And then transmit over the `Websocket` different frames with expected resources and their intervals:

```javascript
{"resource": "temp", "interval": 5, "enabled" : true}
{"resource": "humidity", "interval": 5, "enabled" : true}
```

### MQTT Integration

~~TBD~~

~~devices/smart\_irrigation/resources/temp?interval=5~~

### Different streaming intervals

There can be conflicts if different sources requires different sampling intervals for the same resource. For example, a data storage configured to write a resource every minute, and a dashboard requiring real-time data from from the same resource every 10 seconds. There are different workarounds here that can be implemented in the server, as the client should remain as simple as possible:

* Forbid multiple`Start Stream` over a resource with different sampling intervals, and force the client to define different resources for each data-sink/interval, i.e., one for the data storage, and another for the dashboard, so there are not conflicts as the resource are different.
* Allow multiple `Start Stream` over a resource with different sampling interval, but ignore newer sampling intervals.
* Allow multiple `Start Stream` and dynamically compute the Greatest Common Divisor \(GCD\) between stream requests, reconfigure the device stream interval, and provide data to each source at the specified interval. This is the most complex approach, and is the one implemented in [Thinger.io](https://thinger.io). In this case, if the dashboard A requires data every 6 seconds, and dashboard B every 9 seconds, the server computes the GCD of both sources \(3\) and configures the device to transmit every 3 seconds.  The dashboard A will get data every 6 seconds, and B every 9. If one source is added or removed, the process is repeated to accommodate to the new situation.

### Sampling intervals and events subscriptions 

There is another use case where a data sink may require to receive a resource data periodically, i.e., to store it, and other data sink require only events, i.e., raised events by the device. ~~TBD~~

