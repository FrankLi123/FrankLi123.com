---
layout: post
title: "ActivityPub协议：去中心化社交网络的基石"
date: 2023-10-26 10:00:40
type: article
language: chinese
category: decentralization
blurb: "让我们来了解ActivityPub协议"
og_image: /assets/img/content/article/activitypub/activitypub_1.jpeg
---

<img src="{{ "/assets/img/content/article/activityPub.png" | relative_url }}" alt="bay" class="post-pic"/>
<br />
<br />

ActivityPub 是个很有意思的社交网络协议。它允许了不同的社交网络平台进行数据的传输交互，从而形成了一个大的非中心化的社交平台。随着越来越多的产品都和它相关，在这里我想简单的介绍一下ActivityPub，分享一下我的理解。

<br />

#### 目录
1. [**为什么需要有ActivityPub这样的协议呢？**](#为什么需要有activitypub这样的协议呢？)
2. [**ActivityPub的具体实现**](#activitypub的具体实现)
    * [**Actor 对象 - 用户如何与网络交互**](#actor-对象---用户如何与网络交互)
    * [**Data 对象 - 协议中的数据结构**](#data-对象---协议中的数据结构)
    * [**数据传输 - 用户之间的数据传输机制**](#数据传输---用户之间的数据传输机制)
3. [注释](#注释)

#### **为什么需要有ActivityPub这样的协议呢？**

什么是网络协议呢？协议也就是网络数据传输的一种规范，它负责制定数据在一个网络传输的规则，例如数据是如何从网络的一端传到另一端的。这要先说说社交网络的背景。互联网上有很多有名的中心化社交媒体产品, 例如我们熟知的instagram、twitter等。它们都有大量活跃用户，运营的公司掌管着这些产品中用户的个人数据、平台的发放的信息内容等。

许多人想要一个去中心化的社交网络, 其中的一个实现方法就是利用 "**联邦网络**" - 的由分散式的多个社交网络组成的一个大型社交网络。 而ActivityPub 协议可以作为搭建分散式小网络的桥梁。 只要社交网络的服务器都支持ActivityPub，那么就可以像在**同一个平台**一样信息交流。

ActivityPub协议分为**两部分**。一部分制定了**服务器之间**的信息传输规则。而另一部分制定了**用户和服务器之间**的信息传输规则，允许用户参与网络进行一些活动, 例如发送信息给另一个用户或是获取追踪的人的最新发布消息等。 你可以自己部署一个应用ActivityPub协议的服务器，作为唯一的用户去和其他的服务器分享信息或获取他人信息。你也可以注册成为一个支持ActivityPub协议的服务器用户去做同样的事情。 现在有很多支持ActivityPub的服务器可以选择。举个例子,web3的一些去中心社交ap "**Mastodon**"或"Misskey" 都是联邦网络平台，它们主要提供软件用来搭建一个支持ActivityPub的服务器。当然，在这个平台上也有人运行大型的、专给他人提供使用的服务器, 这样我们可以直接在它们上注册并成为用户。

<br />

#### **ActivityPub的具体实现**

让我们详细探讨一下ActivityPub的技术实现。

<img src="{{ "/assets/img/content/article/activityPubRoute.png" | relative_url }}" alt="bay" class="post-pic"/>
<br />

##### **Actor 对象 - 用户如何与网络交互**

ActivityPub支持**actor模型**。actor是服务器上的一个实体，负责促进用户与外部网络的交互。这个actor包含了**inbox**、**outbox**、following、followers等基本的数据结构。比如，inbox帮助用户接收来自整个外部网络的与你相关的活动，例如你关注的用户的新帖子，或者你的帖子被点赞。而outbox则存储将要发送到外部网络的用户操作活动，例如最近发布的帖子, 你关注的活动。

<br />

##### **Data 对象 - 协议中的数据结构**

ActivityPub协议规定了在网络上传输的数据格式，它使用**ActivityStreams**数据格式，这是一种常见的JSON格式，被称为**Objects**。Objects可以表示各种**活动**，用于各种社交场景下的实际用例，例如创建笔记/帖子、点赞、关注或在网络上发送消息。支持ActivityPub的服务器帮助用户生成Objects，并在与网络交互期间管理它们。此外，一些联邦平台（如Mastodon）会在ActivityPub格式的基础上增加新的字段，以满足其社交服务的特定需求。总的来说，ActivityPub格式为整个联邦网络提供了基本的数据结构。

<br />

##### **数据传输 - 用户之间的数据传输机制**

假设服务器1上有用户A，服务器2上有用户B。目标是让用户B接收到用户A的最新活动。通过协议有多种数据传输方式：

1. 如果用户B关注了用户A，A的actor会使用**WebFinger协议**（后面解释）向B的actor outbox发送一个Object类型的活动，使B能够接收更新。
2. 服务器1和服务器2建立了**联邦关系**，两个服务器会互相读取对方的Activity Stream，从而更新各自服务器上的actors。用户B的actor inbox最终会更新并接收到用户A的更新。
3. 服务器1和服务器2可能使用了**中继服务**，服务器1将公开消息传播到其他服务器，包括服务器2。因此，用户B的actor接收到新的Object。

我们稍微讨论下方法1中提到的**WebFinger**协议。这个协议帮助ActivityPub服务器在服务器域中查找和识别特定用户，帮助在不同的联邦网络服务器上的用户之间建立桥梁。它被用来找到用户的actor资料URI，其中包含inbox和outbox的URL。这样，actor可以通过向目标inbox/outbox URL发送HTTPs请求来与该用户交互，例如发送消息或读取更新。

以上就是对ActivityPub的基本介绍，之后会详细讲述有关ActivityPub与Mastodon的内容。

<br />

##### 注释

[^1]: 这是一个注释！