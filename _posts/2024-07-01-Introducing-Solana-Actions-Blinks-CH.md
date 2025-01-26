---
layout: post
title:  "Solana Actions 和 Blinks：搭建了 Web2 通往 Web3 Solana 世界的桥梁"
date:   2024-07-06 00:00:40
type: article
language: chinese
category: crypto
blurb: "今天，我将详细介绍一下 Solana 最近很火的新功能：Solana Actions 和 Blinks。"
og_image: /assets/img/content/article/7_6_solana_actions/solana_actions_1.jpeg
author: LowkeySmile
---

<img src="{{ "/assets/img/content/article/7_6_solana_actions/solana_actions_1.jpeg" | relative_url }}" alt="Solana Actions 和 Blinks" class="post-pic"/>
<br />
<br />

今天，我将详细介绍一下 Solana 最近很火的新功能：**Solana Actions** 和 **Blinks**。可能大家已经听说过它们了，这些创新使 Web2 用户更容易参与 Web3 Solana 上的内容和活动。

<br />

# 为什么需要 Solana Actions？

让我们先讨论一下没有 Solana Actions 时是什么样的。以前用户必须访问去中心化应用程序（dApp），通过嵌入的数字钱包进行一些 Solana 的链上活动。而现在通过 Solana Actions，Web3 开发人员能从互联网上的许多平台上为其用户提供服务，而无需让他们访问专门的 dApp 页面。这使得用户交互更加方便和直接了。

想象下有人在 X（Twitter）上发布帖子推广他们的去中心化交易所（DEX）。如果用户在 Phantom Wallet 等应用程序上启用了 Solana Actions，他们可以直接体验 Solana Actions。这则 X 帖子会变成一个包含图像和按钮的互动界面，允许用户直接在帖子上进行内容互动而无需访问任何外部网站。打个比方，用户只需点击标有“获取 1 SOL”的按钮即可用其他币来兑换。这就是 Solana Actions 的神奇之处。

<br />

# 但是 Solana Actions 和 Blinks 是如何实现这一点的呢？

让我们来看一下 Solana Actions 和 Blinks 的官方定义。

**Solana Actions** 是一组 API 标准，定义如何处理 HTTP 请求并响应交易相关的信息和其他显示内容例如按钮和图片。可以将“**Solana Actions**”理解为定义了**Action 客户端**和**Action 提供者**如何交互的规则（后续会介绍什么是**Action 客户端**和**Action 提供者**）。

**Solana Blinks** 是提供**用户界面**的客户端应用，也就是**Action 客户端**。它们使用 Solana Action API 标准与 **Action 提供者**进行交互。这些**用户界面**可以包括图形和按钮等，为了方便用户直接进行互动。Solana Blinks 作为**中介者**，在 Solana 服务提供者和 Web2 用户之间架起桥梁，使链上活动可以直接在 Web2 平台上进行。

<br />

<img src="{{ "/assets/img/content/article/7_6_solana_actions/solana_actions_2.png" | relative_url }}" alt="Solana Actions 技术流程图" class="post-pic"/>

<br />

上面这张图是来自官网的技术流程图。我们稍微讨论下该过程基本工作原理。我们可以将一些链上活动视为‘**actions**’，例如‘用 1 SOL 兑换一些加密货币’或‘捐赠 5 SOL 给某人’。任何负责这些链上服务的个体（例如 DApp 开发者）都将作为**Action 提供者**来处理**actions**请求。

**Actions 就像 API 端点一样。** 根据 Solana Actions API 标准，它们由**Action 提供者**托管在可公开访问的 **Actions URLs** 上，由各种**Action 客户端**进行访问。需要注意的是：Action 提供者使用 Solana Web3.js 和 Solana RPC 端点实现 Action API 处理请求。当 Action 客户端使用适当的 Actions URLs 并以正确的模式发出请求给**Action 提供者**时，它们可以交互并处理一些为链上活动准备的信息，例如发送用户的公钥来获取未签名的交易以进行后续操作。

在流程图中有**两种类型的请求**：

1. **GET 请求**：检索 URL 上有的 actions 详细信息，使 Action 客户端了解有哪些活动可用。
2. **POST 请求**：涉及与特定 action 相关的操作，例如发送用户的公钥以生成交易签名等。

**Action 客户端** 首先使用**GET 请求**与 **Action 提供者** 交互，并获取有关用户可用的 actions 的信息。然后，它使用**POST 请求**来帮助用户与 **Action 提供者**进行某个 action 操作。

<br />

<img src="{{ "/assets/img/content/article/7_6_solana_actions/solana_actions_3.png" | relative_url }}" alt="Solana Actions 示例" class="post-pic"/>

<br />

## 再聊聊 X 上的 Solana Actions 例子

让我们再来看一下在 X 上的 Solana Actions 示例，可能会让上面的概念变得更清楚易懂。在这个场景中，Phantom Wallet 作为 Action 客户端，而 Jupiter DEX 是 Action 提供者。当你使用 Chrome 浏览器浏览 X 并在 Jupiter DEX 的帖子里遇到一个 Action URL，且你的 Phantom Wallet 已启用 Solana Action 支持时，你会看到该 URL 转变为带有按钮的用户界面。这是因为 Phantom Wallet 发出了一个 GET 请求并显示了渲染的元数据。如果用户点击按钮选择一个 Action，Phantom Wallet 会发送一个相关的 **POST** 请求给服务提供者。然后用户可以就在这个页面继续执行其他步骤来批准并完成链上交易。

需要注意的一点是，那些 Web2 平台不负责为 Solana Actions 执行 actions 相关的东西；它们只是显示 Actions 的效果。像 Phantom Wallet 这样的客户端应用程序会检测相关链接并替你发出必要的请求。

<br />

## Solana Blinks 中的链接注册

并不是所有的 Web3 项目都可以使用 **Solana Blinks**。在 Solana 中有一个名为 **Dialect** 的公共区块链链接注册表。这个注册表验证每个想要成为 Blink 的合作伙伴，以确保它们没有安全问题。**Dialect 也**帮助确定和审核这些服务要提供的 **Actions 服务**。

目前，大多数 Web3 的交际仍然在受欢迎的 Web2 平台上进行，这些平台拥有大量的 Web3 用户群。Solana 可以通过这个新功能吸引更多用户和开发者进入其生态系统。因此，更多的 Web3 应用程序可能会申请成为 Solana Action 提供者，更多的 Web3 中间件工具（如嵌入式钱包）也将参与这一运动。

<br />

## **需要考虑的问题**

但是，还有一些其他相关的问题需要考虑：

- **安全问题**：虽然 Blinks 需要注册和批准，但如果用户使用的 Blinks 或者 Action 提供者的服务被黑客攻击，前端用户的访问被引导至恶意网站怎么办？作为一个曾在扩展钱包中损失过资金的人，我对在线操作非常谨慎。
- **Blinks 的可扩展性**：这些 Blinks 的**可扩展性**如何？谁决定谁可以成为 Blink 合作伙伴，是否有明确的限制？
- **Web2 服务提供商的态度**：如果在广泛采用后出现更多损害用户利益的问题，Blinks 和那些 Solana dApps 还能否与 **Web2 平台**保持合作？X 还会允许各种用户案例的应用吗？
- **移动用户的便携性**：X 和 Telegram 的许多用户都在使用**移动设备**，而使用嵌入式和扩展钱包并不是很方便。

<br />

## Solana Actions 和 Blinks 的潜在未来应用

我们可能会看到 Actions 和 Blinks 被应用于各种流行的 Web2 平台，不仅限于社交媒体平台，还包括金融服务平台和物品交易平台等。这将使 Web2 用户能够更直接的参与 Solana 活动。此外，我们可能会在游戏中看到 Actions，使玩家可以在**游戏**内直接交易物品。还有许多其他潜在的使用案例需要开发者去发掘。

由于我们生活的许多方面现在都建立在互联网上，采用更适合 Web2 的方法为普通用户打开通往 Web3 的大门是合理且必要的。我们期待 Solana Actions 和 Blinks 的扩展和发展。

<br />