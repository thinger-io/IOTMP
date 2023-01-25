---
description: Internet of Things Message Protocol (IOTMP)
---

# Protocol

## Introduction

An IoT (Internet of Things) protocol is a set of rules and standards that govern communication between devices in an IoT network. These protocols provide the foundation for connecting and communicating with the billions of devices that make up the Internet of Things. They determine how devices connect to the network, how data is transmitted and received, and how security is implemented.&#x20;

IoT protocols are designed to be lightweight, low-power, and efficient, in order to support the large number of devices and limited resources typical of IoT networks. Some common IoT protocols include MQTT, CoAP, and AMQP, but there are many other protocols available, each with its own strengths and weaknesses. The choice of protocol will depend on the specific requirements of the application and the environment in which the IoT network will be deployed.

## IOTMP

IOTMP (Internet of Things Message Protocol) is a lightweight, request-response, and streaming oriented protocol that is designed for use in IoT networks. It is a messaging protocol that allows devices to communicate with a central server or platform, which acts as the hub of the network.

IOTMP is not yet another IoT protocol, as it has been designed with simplicity and performance in mind, but thinking on solving all common IoT usage patterns of a remote device, like sensing, actuating, streaming data, or enabling interoperability with third party services. Take a look to the IOTMP reference implementation to know more about its unprecedented [features](thinger.io-iotmp/features/).

IOTMP is a client-server protocol, where devices that exposes resources (i.e., sensing measurements or actuation controls) are called "clients" and the central server is called the "server." Clients connect to the server and expose their resources, where the server makes them available over over REST API, or websockets. Moreover, clients can interact with server-side resources, i.e., for reading configurations, interacting with third party services (APIs), triggering alarms, subscribing to events, etc.&#x20;

One of the main advantages of IOTMP is that it is designed to be lightweight and efficient, which is important in IoT networks where devices may have limited resources. It also has a small footprint and is easy to implement, making it well suited for resource-constrained devices like sensors or microcontrollers. Currently, IOTMP is available for different programming languages, including Arduino, C++, NodeJs, Python, and Javascript for the web.

IOTMP also provides a good level of security, it uses a combination of username and password to authenticate clients and also a SSL/TLS encryption for secure communication.

Another advantage of IOTMP is its ability to handle a large number of devices and handle a high volume of data, which makes it scalable for large IoT deployments.

IOTMP is widely used in various IoT applications such as industrial automation, smart home, and energy management systems.



