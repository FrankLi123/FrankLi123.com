---
layout: post
title: "The Future of Decentralized Communication: Federation Instant Messaging (IM) Protocols, from XMPP to Matrix"
date: 2024-07-16 00:00:00
type: article
language: english
category: decentralization
blurb: "Let's talk about the future of decentralized social communication."
og_image: /assets/img/content/article/7_16_im_protocol/xmpp1.jpeg
author: LowkeySmile
---


As instant messaging has become a significant part of our daily lives, it's essential to explore alternative messaging options to WhatsApp and Facebook Messenger, particularly in terms of **decentralization** and **personal privacy**. Today, let's delve into popular **federated instant messaging protocols**.

Many of you may already be familiar with federated networks and communication. In brief, a **federated network** is a decentralized system where individuals can use independent servers to communicate and share data with one another. No centralized authority controls the communication service.

#### Table of Contents
1. [**XMPP**](#xmpp)
    - [XMPP Architecutre](#architecture)
    - [key problems](#key-problems)
2. [**Matrix**](#matrix)
    - [Matrix Features](#matrix-features)
    - [Communication Design](#event-graph-and-rooms)
    - [End-to-End Encryption](#end-to-end-encryption)
3. [**Conclusion**](#conclusion)

# **XMPP**

<img src="{{ "/assets/img/content/article/7_16_im_protocol/xmpp1.jpeg" | relative_url }}" alt="federation" class="post-pic"/>

The first protocol we'll introduce is **XMPP (Extensible Messaging and Presence Protocol)**. Born in 1999 during the era of PCs, this internet communication protocol is based on XML data. While it supports the transmission of various types of data, we will focus specifically on its use in **instant messaging**.



### Architecture:
Here is a flowchart to illustrate the communication flow.

<img src="{{ "/assets/img/content/article/7_16_im_protocol/xmpp3.png" | relative_url }}" alt="federation" class="post-pic"/>

(source: https://www.cometchat.com/blog/xmpp-extensible-messaging-presence-protocol)

Similar to the **Simple Mail Transfer Protocol (SMTP)** used in email, **XMPP** features an architecture consisting of **clients, servers,** and **gateway services** for message communication. A client registered on one XMPP server can communicate with another client on a different XMPP server through inter-server communication. The gateway service acts as an additional server type, integrating other XMPP-supported services into the XMPP messaging environment, allowing users to communicate with XMPP clients using their email.

The data transmitted in this flow is **Extensible Markup Language (XML)**, which resembles HTML. When users send messages to each other, they actually add more data into a shared XML stream that starts and ends with `<stream>` tags. The basic units of communication in XMPP are **XML stanzas**, which are sub-attributes included in an XML data stream. During real-time communication, the **XML data stream grows larger** as more stanzas are included, until the communication session ends with a `</stream:stream>` tag.

Below is an example of an XML data stream in communication.

<img src="{{ "/assets/img/content/article/7_16_im_protocol/xmpp2.png" | relative_url }}" alt="federation" class="post-pic"/>
(source: IBM, https://developer.ibm.com/tutorials/x-xmppintro/)

The XMPP protocol was one of the earliest to establish federation in instant messaging. However, it exposed some **key problems** that are worth discussing.

### Key Problems:
**Communication Efficiency**
- **XML data** contains more **redundant** information compared to JSON, which is also highly suitable for text messages.
- Although XMPP is an open standard with great flexibility and extensibility, it requires additional internet interactions to determine non-core elements, making it inefficient.

**Security Concerns**
- Security remains a concern for the XMPP protocol, which was not a primary focus in its original design.
- Ensuring that no one can intercept and decrypt XMPP messaging packets is crucial for maintaining secure communication.

# **Matrix**

Now, it's time to introduce a more recent federated communication protocol: **Matrix**. This protocol addresses the two main concerns left by XMPP with a **more sophisticated design**.

<img src="{{ "/assets/img/content/article/7_16_im_protocol/matrix1.png" | relative_url }}" alt="federation" class="post-pic"/>

**Matrix** is an open standard communication protocol for instant messaging that defines how messages are passed between clients. Instead of using XML data, Matrix transmits messages in JSON format.

### Features
- It enables real-time **multi-person chat rooms**.
- It supports **end-to-end encrypted communication** with specialized cryptographic designs.

In Matrix, all JSON data are referred to as "**events.**" Each event has a specific type, with `m.room.message` being the type for instant messages. There are many other various types of events. Below is an example of a message event:

<img src="{{ "/assets/img/content/article/7_16_im_protocol/matrix3.png" | relative_url }}" alt="federation" class="post-pic"/>


### Event Graph and Rooms
All communication is initiated in **rooms**, where users can send and receive events with one another. Regardless of the number of participants, all communication must take place within a room.

To manage the events exchanged in a room, Matrix uses a special graph structure called the **"event graph."** This structure chronologically orders events created in a room, ensuring the synchronization of messages between multiple participants, backfilling messages for new room participants, and handling other functions efficiently.

Here is a flowchart to illustrate the communication flow and show the architecture:

<img src="{{ "/assets/img/content/article/7_16_im_protocol/matrix2.png" | relative_url }}" alt="federation" class="post-pic"/>



### End-to-End Encryption

The technical implementation of encryption in Matrix is very similar to the cryptographic methods used by Signal. It involves two types of sessions: **Megolm** and **Olm**. Megolm sessions derive a symmetric key used by a pair of users to encrypt and decrypt messages. Olm sessions ensure that interactions within Megolm sessions happen securely.

Below is a simplified diagram illustrating the application of the two sessions in establishing secure communication between clients in a room. This ensures that each user can send and receive messages securely from one another. This is achieved by having multiple secure channels between every two individuals within the room. Consequently, the messages displayed in a chat involve many outbound sessions and key exchanges between a pair of users.

<img src="{{ "/assets/img/content/article/7_16_im_protocol/matrix4.jpeg" | relative_url }}" alt="federation" class="post-pic"/>


When a user enters a room, the first step to being able to send a message is initializing a **Megolm session**. The user starts an outbound Megolm session and generates a shared **Megolm key**. This key is shared with each participant (device) in the room using an event in the `m.room_key` event.

To securely share the Megolm keys with each participant, **Olm sessions** will be used in step 2.

Once the Megolm key is delivered to every participant/device in the room, both the sender and the recipient can derive an asymmetric key (step 3) and decrypt the message encrypted using the same asymmetric key (step 4).

This process ensures the secure delivery of messages between users in a room. **Periodically**, every user will re-initialize an outbound Megolm session to refresh the Megolm key for security purposes. If a client leaves a room, any active outbound Megolm sessions should be invalidated. Similarly, if a new client joins a room, they need to start a Megolm session to send and receive messages in that room.


# **Conclusion**
There's still much more to discuss about Matrix and other future federated instant messaging protocols, but we'll stop here for now. While many factors currently prevent them from being mainstream, the growing awareness of personal privacy in instant messaging will help these federated tools gain prominence. The time for these protocols to become part of the social mainstream is approaching.