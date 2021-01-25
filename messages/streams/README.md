# Resource Streams

The [Run ](../run.md)message is perfectly suited for request/response paradigms. Those messages allows to send a request and receive a response. This is quite useful for sending a request to a device, i.e., to turn on a light, or to query the current power consumption. However, this approach is not optimized if it is necessary a long-lived monitoring over a resource. For example, monitoring every few seconds the temperature and humidity. In this case, a constant polling to the device is not efficient.

To solve this problem, there are other protocols like MQTT where the devices just transmit the information periodically to the broker, and then this information is stored or shown in dashboards. However, this approach is not optimal, as it is assuming that the transferred information will be used somewhere. It does not take into account if the information really requires to be transmitted, i.e., there is an user viewing the dashboard, or there is a data sink storing the information. In large projects, for sure there are several topics and information that is going to nowhere.

This is where the [Streams ](../../definitions.md#stream)comes into play. It enables an endpoint, i.e., the server, to subscribe to a device resource. This way, the server proactively subscribes to device resources if it is necessary. The subscription can be periodical, or just triggered as required \(i.e., an event detected by the device\). In this approach, the target resource is not streamed by default, unless there is a source requesting a streaming, i.e., a user just opened a dashboard or a mobile application, or the server defined a data sink to store the information. It adds extra complexity at the server, but optimizes how the resources are streamed, saving bandwidth and scaling easily under some circumstances.

TODO add diagram

TODO add description about devices opening streams over server

TODO devices opening streams over other devices ? 



## Messages

Streaming functionality has 4 messages defined to start and stop streams, and to send the data associated to a resource from a sampling interval or for an event.

{% page-ref page="start-stream.md" %}

{% page-ref page="stop-stream.md" %}

{% page-ref page="stream-event.md" %}

## Use Cases

TBD

