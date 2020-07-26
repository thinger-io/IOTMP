---
description: >-
  Initiates a long-live stream for transmitting periodic data associated to a
  resource.
---

# Start Stream

The [Run ](../run.md)message is perfectly suited for request/response paradigms. Those messages allows to send a request and receive a response. This is quite useful for sending a request to a device, i.e., to turn on a light, or to query the current power consumption. However, this approach is not optimized if it is necessary a long-lived monitoring over a resource. For example, monitoring every few seconds the temperature and humidity. In this case, a constant polling to the device is not efficient.

To solve this problem, there are other protocols like MQTT where the devices just transmit the information periodically to the broker, and then this information is stored or shown in dashboards. However, this approach is not optimal, as it is assuming that the transferred information will be used somewhere. It does not take into account if the information really requires to be transmitted, i.e., there is an user viewing the dashboard, or there is a data sink storing the information. In large projects, for sure there are several topics and information that is going to nowhere.

This is where the `Start Stream` comes into play. It enables an endpoint, i.e., the server, to subscribe to a device resource. This way, the server proactively subscribes to device resources if it is necessary. The subscription can be periodical, or just triggered as required \(i.e., an event detected by the device\). In this approach, the target resource is not streamed by default, unless there is a source requesting a streaming, i.e., a user just opened a dashboard, a mobile application, or the server defined a data sink to store the information. It adds extra complexity at the server, but optimizes how the resources are streamed, saving bandwidth and scaling easily under some circumstances.

{% hint style="info" %}
**TL;DR**: Allows to request a periodical resource streaming, both at a fixed interval or by events.
{% endhint %}

## Message

### Header

| Field | Value | Description |
| :--- | :--- | :--- |
| **Message Type** | 0x05 | Start Stream |
| **Message Size** | varint | Remaining Message Length |

### Body

| Field | Identifier | Type | Mandatory | Value |
| :--- | :--- | :--- | :--- | :--- |
| **Stream Id** | 0x01 | varint | Yes | Stream identifier to be used to be used within the stream life-time. |
| **Resource**  | 0x02 |  | First Time | A string or array of strings with the resource identifier, i.e., "temperature". It is only mandatory the first time the stream is opened. Following Start Streams over the same Stream Id can be used fo reconfigure the interval, so it is not required to specify again the resource. |
| **Interval** | 0x04 | varint | No | Sampling interval in seconds. If the field is not present or zero,  just allows the target resource to stream the resource as considered, i.e., when there is an event.  |

## Responses

| Message | Description |
| :--- | :--- |
| \*\*\*\*[**Ok**](../ok.md)\*\*\*\* | Should answer with an OK if it is able to stream the requested resource at the specified interval. It must contain the Stream Id specified in this message. |
| \*\*\*\*[**Error**](../error.md)\*\*\*\* | Should answer with an Error if the target resource cannot be streamed at the specified interval. It must contain the Stream Id specified in this message. |

## Stream Messages

| Message | Description |
| :--- | :--- |
| \*\*\*\*[**Stream Sample**](stream-sample.md)\*\*\*\* | If the resource has been configured with a sampling interval, it must send the data using the `Stream Sample` message, that represents a periodical sampling data over the stream.  |
| \*\*\*\*[**Stream Event**](stream-event.md)\*\*\*\* | If the resource has been configured without a sampling interval, it must send the data using the `Stream Event` message, that represents a message over the stream.  |
| \*\*\*\*[**Stop Stream**](stop-stream.md)\*\*\*\* | A `Stop Stream` can be sent anytime during the stream life-time to conclude the streaming. |
| \*\*\*\*[**Start Stream**](start-stream.md)\*\*\*\* | A `Start Stream` can be sent anytime by the requester to reconfigure the sampling interval. In such case, should send only the Stream Identifier and the new Interval. |

## Server Implementation notes

### HTTP/REST API/MQTT

A typical scenario where a `Start Stream` is required is when there is opened a Websocket or Server Sent Event over the server to start listening over a resource information. For example, in Thinger.io, a resource URL is defined as follow:

```text
https://backend.thinger.io/v3/users/alvarolb/devices/smart_irrigation/resources/temp
```

### 

### Different streaming interval

There can be conflicts if different sources requires different sampling intervals for the same resource. For example, a data storage configured to write a resource every minute, and a dashboard requiring real-time data from from the same resource every 10 seconds. There are different workarounds here that can be implemented in the server, as the client should remain as simple as possible:

* Forbid multiple`Start Stream` over a resource with different sampling intervals, and force the client to define different resources for each data-sink/interval, i.e., one for the data storage, and another for the dashboard, so there are not conflicts as the resource are different.
* Allow multiple `Start Stream` over a resource with different sampling interval, but ignore newer sampling intervals.
* Allow multiple `Start Stream` and dynamically compute the Greatest Common Divisor \(GCD\) between stream requests, reconfigure the device stream interval, and provide data to each source at the specified interval. This is the most complex approach, and is the one implemented in [Thinger.io](https://thinger.io). In this case, if the dashboard A requires data every 6 seconds, and dashboard B every 9 seconds, the server computes the GCD of both sources \(3\) and configures the device to transmit every 3 seconds.  The dashboard A will get data every 6 seconds, and B every 9. If one source is added or removed, the process is repeated to accommodate to the new situation.

### Sampling intervals and events subscriptions 

There is another use case where a data sink may require to receive a resource data periodically, i.e., to store it, and other data sink require only events, i.e., raised events by the device. Suppose a resource "A" that provides temperature and humidity, and

