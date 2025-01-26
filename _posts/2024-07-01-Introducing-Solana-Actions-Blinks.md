---
layout: post
title:  "Solana Actions and Blinks: Bridging Web2 and Web3 for Solana Interaction "
date:   2024-07-06 00:00:40
type: article
language: english
category: crypto
blurb: "Today, I will introduce the popular new features Solana Actions and Blinks."
og_image: /assets/img/content/article/7_6_solana_actions/solana_actions_1.jpeg
author: LowkeySmile
---

<img src="{{ "/assets/img/content/article/7_6_solana_actions/solana_actions_1.jpeg" | relative_url }}" alt="Solana Actions and Blinks" class="post-pic"/>
<br />
<br />

Today, I will introduce the popular new features **Solana Actions** and **Blinks**. Some of you may have already heard about them. These innovations make it easier for Web2 users to engage with Web3 content and activities.

<br />

# **Why Are Solana Actions Needed?**

Let's discuss the rationale behind Solana Actions. Traditionally, users had to visit a decentralized application (dApp) to perform on-chain activities with blockchains using their embedded digital wallets. Now, Solana enables Web3 developers to provide users with access to various services directly from anywhere on the internet, without needing to visit a dApp’s page. This makes user interactions more convenient and direct.

For example, imagine someone posts on X (Twitter) to promote their decentralized exchange (DEX). If the user has enabled Solana Actions on an application like Phantom Wallet, they can experience the benefits of Solana Actions directly. The X post becomes an interactive interface with elements like images and buttons, allowing users to engage with the content right on the X platform without needing to visit any external websites. Users can simply click a button labeled 'Get 1 SOL' to exchange it for other cryptocurrencies.

That's the promising and magical aspect of Solana Actions.

<br />

#  **But how do Solana Actions and Blinks make this happen?**

Let’s take a look at the official definitions of Solana Actions and Blinks.

**Solana Actions** are a set of API standards designed to accept HTTP requests and responds with transactions and messages across various contexts, such as buttons and QR codes. Think of ‘**Solana Actions**’ as the rules that define how an **action client** and an **action provider** interact(will introduce meaning of **action client** and **action provider later** ).

**Solana Blinks** are client applications with **user interfaces** that use the Solana Action API to interact with the Solana blockchain. These interfaces can include graphics and buttons, allowing users to engage directly. Solana Blinks serve as **intermediaries** between Solana service providers and Web2 users, enabling on-chain activities to be performed directly on Web2 platforms.

<br />

<img src="{{ "/assets/img/content/article/7_6_solana_actions/solana_actions_2.png" | relative_url }}" alt="Technical Flowchart" class="post-pic"/>

<br />

This is the technical flowchart from the official site. We will briefly discuss how the procedure works at a high level. To understand, we can consider some on-chain activities as **‘actions’**, such as ‘exchange 1 SOL for some cryptocurrency’ or ‘donate 5 SOL to someone’. Any entity (e.g., a DApp developer) responsible for these actions acts as an action provider to handle action requests.

**Actions function like API endpoints.** According to the Solana Actions API standard, they are hosted at publicly accessible **Actions URLs** by an action provider. A quick note: the action provider implements the API handler functions using Solana Web3.js with Solana RPC endpoints. When the action client makes requests using the appropriate Actions URLs and in the correct schema, it can interact with and retrieve the necessary information, such as unsigned transactions for further actions.

There are **two types of requests** in the flowchart:

1. **GET requests** retrieve details about the actions available at the URL, allowing the action client to understand which activities are available.
2. **POST requests** involve operations related to a specific action, such as sending a user’s public key to generate a transaction to sign.

The action client first uses **GET requests** to interact with the action provider and obtain information about the available actions for the user. Then, it uses **POST requests** to facilitate user interactions with the action provider for those on-chain operations.

<br />

<img src="{{ "/assets/img/content/article/7_6_solana_actions/solana_actions_3.png" | relative_url }}" alt="Solana Actions Example on X" class="post-pic"/>

<br />

## **Example Revisited: Solana Actions on X**

Let’s revisit the Solana Actions example on X. In this scenario,  **Phantom Wallet** acts as the  **action client**, and  **Jupiter DEX** is the  **action provider**. When you browse X with a Chrome browser and encounter an action URL in a Jupiter DEX tweet, and your Phantom Wallet has Solana Action support enabled, you will see the URL transform into a user interface with buttons. This happens because Phantom Wallet made a **GET request** and displayed the rendered metadata. If the user clicks a button to select an action, Phantom Wallet sends a related **POST** request. The user can then proceed with additional steps to approve and complete the transaction on-chain.

It's important to note that major Web2 platforms do not perform the work for Solana Actions; they merely display the actions. Client applications, like Phantom Wallet, detect the relevant links and make the necessary requests on your behalf.

<br />

## **Registry of Links in Solana Actions:**

Not just any Web3 project can use Solana Blinks. There is a public registry of blockchain links in Solana called **Dialect**. This registry verifies every partner wanting to become a Blink to ensure there are no security issues. It helps these services register the actions they need, which will be provided by these service providers.

Currently, most Web3 discussions still take place on popular Web2 platforms, which have a large Web3 user base. This presents a great opportunity for Solana to attract more users and developers into its ecosystem. As a result, more Web3 applications are likely to apply to become Solana Action providers, and more Web3 middleware tools, like embedded wallets, will participate in this movement.

<br />

## **Issues to Consider:**

But there are some other issues to consider:

1. **Security Concerns**: Although Blinks need to be registered and approved, what happens if the Blinks a user uses get hacked and users are directed to malicious websites? As someone who has lost money through an extension wallet before, I am very cautious about online operations.
2. **Scalability of Blinks**: How scalable are these Blinks? Who decides who can become Blink partners, and are there clear limitations?
3. **Attitudes of Web2 Service Providers**: If more issues arise that harm users' interests after widespread adoption, will Blinks and those Solana dApps still be able to maintain cooperation with Web2 platforms? Will X still allow for a variety of user cases?
4. **Portability for Mobile Users**: Many users of X and Telegram are on mobile, where using embedded and extension wallets isn’t very convenient.

<br />

## **Potential Future Applications of Solana Actions and Blinks:**

We may see Actions and Blinks being used on various popular Web2 platforms beyond social media, such as financial services platforms and item trading platforms. This will enable Web2 users to participate in Solana activities conveniently. Additionally, we might see Actions in games, allowing players to trade items directly within the game. There are numerous other potential use cases.

As many aspects of our lives are now built on the internet, using a more Web2-friendly approach to open the door to Web3 for regular users is both reasonable and necessary. We look forward to the expansion and development of Solana Actions and Blinks.

<br />