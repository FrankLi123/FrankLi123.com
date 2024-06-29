---
layout: post
title:  "Introducing ActivityPub Protocol: The Keystone in Federated Network"
date:   2024-06-28 10:00:40
type: article
language: english
blurb: "Let's talk about ActivityPub."
og_image: /assets/img/content/article/activityPub.png
---

<img src="{{ "/assets/img/content/article/activityPub.png" | relative_url }}" alt="bay" class="post-pic"/>
<br />
<br />

ActivityPub is an interesting and promising social networking protocol. It enables data transfer between different social networking platforms, creating a broad decentralized social ecosystem. As more and more social products integrate this protocol, I want to introduce it and share my understanding of its potential.

<br />

#### Table of Contents
1. [**Why do we need the ActivityPub protocol?**](#why-do-we-need-the-activitypub-protocol)
2. [**Implementation of ActivityPub**](#implementation-of-activitypub)
    * [**Actor Object**](#actor-object---how-users-interact-with-the-network-in-activitypub)
    * [**Data Object**](#data-object---the-format-of-the-protocol-data)
    * [**How Data is Transmitted**](#how-data-is-transmitted-from-one-server-to-another)
3. [Footnotes](#footnotes)

#### **Why do we need the ActivityPub protocol?**

What is a networking protocol? A networking protocol is a set of rules for data transmission over a network. It dictates how data is transferred from one end of the network to the other.

Let’s talk about the background of social networks. There are many popular centralized social media platforms, such as Instagram and Twitter. These platforms have a large number of active users, but the companies that own them control users’ personal data and the content distributed on the platform.

On the other hand, many people desire a decentralized social network. One way to achieve this is through a “**federated network**,” which is a large network composed of multiple decentralized social networks. The ActivityPub protocol can build these decentralized small networks and serve as a bridge to connect them. As long as the servers support ActivityPub, information can be exchanged as if they are on the same platform.

The ActivityPub protocol has two parts. One part defines the rules for data transmission **between servers**. The other part defines the rules for data transmission **between users and servers,** allowing users to participate in the network by performing activities such as sending messages to others or fetching the latest posts from others. You can deploy your own server that implements the ActivityPub protocol to interact with the federated network as a sole user. Alternatively, you can register as a user on an ActivityPub-supported server to do the same. There are many kinds of servers that support ActivityPub. For instance, web applications like **Mastodon** and Misskey are federated network platforms that primarily provide software to host servers supporting social communication via ActivityPub. One can also register to become a user on the large servers run on these platforms and communicate in the network.

<br />

#### **Implementation of ActivityPub:**

Let’s talk more about the technical implementation aspects of ActivityPub, using Twitter-like concepts to illustrate these ideas.

<img src="{{ "/assets/img/content/article/activityPubRoute.png" | absolute_url }}" alt="bay" class="post-pic"/>


<br />

##### **Actor Object - How Users Interact with the Network in ActivityPub**:

ActivityPub supports the **actor model**. An actor is an entity on the server responsible for facilitating user interactions with the external network. This actor has several basic data structures: inbox, outbox, following, and followers. Specifically, the inbox helps a user receive information from the external network, such as new posts from followed users or likes on their posts. The outbox stores activities that the user has performed and will send to the external network, such as recent posts or follow activities.

<br />

##### **Data Object - The Format of the Protocol Data**:

The ActivityPub protocol specifies the format of data transmitted over the federated network. It uses the **ActivityStreams** data format, a common JSON format referred to as **Objects**. Objects can represent various **activities** for different use cases, such as creating a note/post, liking, following, or messaging on the network. A server that supports ActivityPub helps users generate Objects and manage them during interactions with the network. Additionally, some federated platforms like Mastodon add new fields to the ActivityPub format to meet the unique needs of their social services. Overall, the ActivityPub format provides the basic data structure for the entire federated network.

<br />

##### **How Data is Transmitted from One Server to Another**:

Assuming there is a user A on server 1 and a user B on server 2. The goal is for user B to receive the latest activities of user A. There are multiple ways for data transmission over the protocol:

1. If user B follows user A, A's actor sends an activity in Object type to B's actor outbox using the **WebFinger protocol** (explained later), allowing B to receive updates.
2. Server 1 and Server 2 establish a **federated relationship**, and both servers periodically read each other's Activity Stream to update their actors. User B’s actor inbox will eventually be updated and receive user A’s updates.
3. Server 1 and Server 2 might use a **relay service**, where Server 1 propagates public messages to other servers, including Server 2. As a result, User B’s actor receives the new Object.

Let’s talk about the **WebFinger protocol** mentioned in method 1. The WebFinger protocol helps ActivityPub servers find and identify a specific user in a server domain, essentially building bridges between users on different federated network servers. It assists an actor in finding a user’s actor profile URI, which contains the inbox and outbox URL. This way, the actor can interact with that user by making requests to the targeted inbox/outbox URL, such as sending messages or reading updates.

This is a general overview of ActivityPub. More detailed discussions about ActivityPub and Mastodon will follow next.

<br />

##### FOOTNOTES

[^1]: This is a note!
