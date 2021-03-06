---
title: Welcome
order: -100
---

# Index

In addition to the docs here, which are guides to building on Bantu, you'll also see a link at the bottom of the left nav to the API Reference. You should check those out, too: that's a resource most developers consult as they build on Bantu.

A rundown of what's here:

## Tutorials

If you’re new to Bantu and want to get an overview of the network, this is where to start. The early tutorials will show you how to do some basic things like create an account and make payments. The later tutorials cover more advanced topics like Bantu smart contracts. If you want to issue an asset or build an app, you're better served checking the sections dedicated to those paths.

## Issue Assets

Bantu is a multi-currency network by design. The ability to issue assets is fundamental to Bantu, and it's something you can do quickly, safely, and in a few lines of code. Once you've issued an asset, you can also publish canonical information about it for wallets and consumers, control access to it by setting simple flags, and make it available for trade on the Bantu decentralized exchange. This section will show you how.

## Anchor Assets

Organizations can connect assets issued on Bantu with external banking and payment systems, allowing users and businesses to transfer assets onto or through the Bantu network. Specifically, organizations can **anchor** assets issued on the Bantu network by facilitating 1-1 trades for the off-chain representation of the tokenized asset.

### Deposits & Withdrawals

For example, a USD anchor could accept $1000 USD from a customer's wire transfer and send 1000 USDX tokens to the customer's Bantu account. Conversely, another customer could send USDX tokens to the anchor on Bantu and expect an incoming $1000 USD wire transfer from the anchor. These kinds of deposit and withdrawal operations are facilitated by wallet applications and SEP-24 anchor servers.

### Cross-border Payments

Anchors can also facilitate payments made through Bantu instead of simply on Bantu.

For example, a customer could want to send $1000 USD worth of EUR to a friend's bank account in Germany. Anchor A could collect the sending and receiving customer's information, make a USD-&gt;EUR path payment on Bantu to Anchor B \(in Germany\), and Anchor B could deposit the funds into the recipent's bank account.

## Build Apps

Bantu is a self-serve distributed ledger that you can use as a backend to power all kinds of apps and services. Any app built on Bantu relies on the same basic functions: key storage, account creation, transaction signing, and queries to the Bantu database. This section of the docs will walk you through the process of building a basic wallet that does all those things, and will show you how to add features to it like the support for in-app deposits and withdrawals from anchors.

## Run a Core Node

This section explains the technical and operational aspects of installing, configuring, and maintaining a Bantu Core node, which is a server that connects to the Bantu peer-to-peer network to keep a common distributed ledger. You don’t have to run a node to get started on Bantu, but you will likely want to if you're in production, need high-availability access network, or want to help increase network health and decentralization.

## Run an API Server

Most developers access the network using Horizon, the Bantu API. It takes the performance-oriented data structures from Bantu Core and converts them into a friendlier format. If you're running your own Bantu Core node and using it to submit transactions or get network data, you will likely also want to run your own Horizon instance, and this section will show you how. If you're just looking to use Horizon \(vs. setting up a Horizon server\), consult the API Reference.

## Software and SDKs

This is where you'll find all the Bantu SDKs. There are a lot of them, and they're all pretty well maintained and documented, so you should be able to build on Bantu in your language of choice. This section is also home to some tools and reference implementations created and maintained by the Bantu Development Foundation to kickstart development.

## Glossary

This section defines all the terms and explains all the concepts germane to Bantu. Use it to look up a word, or to dig deeper into nitty-gritty details.

