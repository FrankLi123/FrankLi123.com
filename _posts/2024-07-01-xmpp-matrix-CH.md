---
layout: post
title: "去中心化通信的未来：从XMPP到Matrix的联邦即时通讯协议演进"
date: 2024-07-16 00:00:00
type: article
language: chinese
category: decentralization
blurb: "让我们探讨去中心化社交通信的未来。"
og_image: /assets/img/content/article/7_16_im_protocol/xmpp1.jpeg
author: LowkeySmile
---

在即时通讯已成为我们日常生活重要组成部分的今天，探索WhatsApp和Facebook Messenger之外的替代通讯方案变得尤为重要，特别是在**去中心化**和**个人隐私**方面。今天，让我们深入了解一下流行的**联邦即时通讯协议**。

很多人可能已经熟悉联邦网络和通信的概念。简单来说，**联邦网络**是一个去中心化系统，用户可以使用独立的服务器相互通信和共享数据。没有中心化的权威机构控制通信服务。

#### 目录
1. [**XMPP协议**](#xmpp协议)
    - [XMPP架构](#架构)
    - [主要问题](#主要问题)
2. [**Matrix协议**](#matrix协议)
    - [Matrix特性](#matrix特性)
    - [通信设计](#事件图和聊天室)
    - [端到端加密](#端到端加密)
3. [**总结**](#总结)

# **XMPP协议**

<img src="{{ "/assets/img/content/article/7_16_im_protocol/xmpp1.jpeg" | relative_url }}" alt="federation" class="post-pic"/>

首先介绍的是**XMPP（可扩展消息与存在协议）**。这个诞生于1999年PC时代的互联网通信协议基于XML数据。虽然它支持各种类型的数据传输，但我们将特别关注其在**即时通讯**中的应用。

### 架构：
下面是一个说明通信流程的流程图。

<img src="{{ "/assets/img/content/article/7_16_im_protocol/xmpp3.png" | relative_url }}" alt="federation" class="post-pic"/>

(来源: https://www.cometchat.com/blog/xmpp-extensible-messaging-presence-protocol)

类似于电子邮件使用的**简单邮件传输协议（SMTP）**，**XMPP**的架构由**客户端**、**服务器**和**网关服务**组成。在一个XMPP服务器上注册的客户端可以通过服务器间通信与另一个XMPP服务器上的客户端通信。网关服务作为一种额外的服务器类型，将其他支持XMPP的服务集成到XMPP消息环境中，允许用户使用电子邮件与XMPP客户端通信。

在这个流程中传输的数据是**可扩展标记语言（XML）**，类似于HTML。当用户相互发送消息时，实际上是在以`<stream>`标签开始和结束的共享XML流中添加更多数据。XMPP中的基本通信单位是**XML节**，它们是包含在XML数据流中的子属性。在实时通信过程中，随着包含更多节，**XML数据流会变得更大**，直到通信会话以`</stream:stream>`标签结束。

下面是通信中XML数据流的示例。

<img src="{{ "/assets/img/content/article/7_16_im_protocol/xmpp2.png" | relative_url }}" alt="federation" class="post-pic"/>
(来源: IBM, https://developer.ibm.com/tutorials/x-xmppintro/)

XMPP协议是最早在即时通讯中建立联邦制的协议之一。然而，它暴露了一些值得讨论的**主要问题**。

### 主要问题：
**通信效率**
- 与同样适用于文本消息的JSON相比，**XML数据**包含更多**冗余**信息。
- 虽然XMPP是一个具有很大灵活性和可扩展性的开放标准，但它需要额外的互联网交互来确定非核心元素，这使得它效率不高。

**安全性问题**
- 安全性仍然是XMPP协议的一个问题，这在其最初设计中并不是主要关注点。
- 确保没有人能够拦截和解密XMPP消息包对于维护安全通信至关重要。

# **Matrix协议**

现在，让我们来介绍一个更新的联邦通信协议：**Matrix**。这个协议通过**更复杂的设计**解决了XMPP留下的两个主要问题。

<img src="{{ "/assets/img/content/article/7_16_im_protocol/matrix1.png" | relative_url }}" alt="federation" class="post-pic"/>

**Matrix**是一个用于即时通讯的开放标准通信协议，它定义了消息如何在客户端之间传递。Matrix使用JSON格式而不是XML数据传输消息。

### Matrix特性
- 支持实时**多人聊天室**
- 通过专门的加密设计支持**端到端加密通信**

在Matrix中，所有JSON数据都被称为"**事件**"。每个事件都有特定的类型，其中`m.room.message`是即时消息的类型。还有许多其他各种类型的事件。下面是一个消息事件的示例：

<img src="{{ "/assets/img/content/article/7_16_im_protocol/matrix3.png" | relative_url }}" alt="federation" class="post-pic"/>

### 事件图和聊天室
所有通信都在**聊天室**中发起，用户可以在其中相互发送和接收事件。无论参与者数量多少，所有通信都必须在聊天室内进行。

为了管理聊天室中交换的事件，Matrix使用一种特殊的图结构，称为**"事件图"**。这种结构按时间顺序排列聊天室中创建的事件，确保多个参与者之间的消息同步，为新的聊天室参与者补充消息，并有效处理其他功能。

下面是一个说明通信流程和架构的流程图：

<img src="{{ "/assets/img/content/article/7_16_im_protocol/matrix2.png" | relative_url }}" alt="federation" class="post-pic"/>

### 端到端加密

Matrix中加密的技术实现与Signal使用的加密方法非常相似。它涉及两种类型的会话：**Megolm**和**Olm**。Megolm会话派生出一个对称密钥，用户对可以使用该密钥加密和解密消息。Olm会话确保Megolm会话中的交互安全进行。

下面是一个简化的图表，说明了两个会话在建立聊天室内客户端之间安全通信中的应用。这确保每个用户都可以安全地相互发送和接收消息。这是通过在聊天室内每两个个人之间建立多个安全通道来实现的。因此，聊天中显示的消息涉及用户对之间的许多出站会话和密钥交换。

<img src="{{ "/assets/img/content/article/7_16_im_protocol/matrix4.jpeg" | relative_url }}" alt="federation" class="post-pic"/>

当用户进入聊天室时，能够发送消息的第一步是初始化**Megolm会话**。用户启动出站Megolm会话并生成共享的**Megolm密钥**。这个密钥通过`m.room_key`事件与聊天室中的每个参与者（设备）共享。

为了安全地与每个参与者共享Megolm密钥，第2步将使用**Olm会话**。

一旦Megolm密钥传递给聊天室中的每个参与者/设备，发送者和接收者都可以派生非对称密钥（第3步）并解密使用相同非对称密钥加密的消息（第4步）。

这个过程确保了聊天室用户之间消息的安全传递。**定期地**，每个用户都会重新初始化出站Megolm会话以刷新Megolm密钥以确保安全。如果客户端离开聊天室，任何活动的出站Megolm会话都应该失效。同样，如果新客户端加入聊天室，他们需要启动Megolm会话才能在该聊天室中发送和接收消息。

# **总结**
关于Matrix和其他未来的联邦即时通讯协议还有很多可以讨论的内容，但我们暂时就到这里。虽然目前有许多因素阻止它们成为主流，但人们对即时通讯中个人隐私的日益关注将帮助这些联邦工具获得重要地位。这些协议成为社交主流的时机正在临近。 