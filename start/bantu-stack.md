---
title: The Bantu Stack
order: 10
---

# Bantu Stack

Fundamentally, Bantu is a collection of Bantu Core nodes, which are computers that keep a common ledger of accounts and balances, listen for incoming transactions, and, using the Bantu Consensus Protocol, agree to apply a valid set of those transactions to update the ledger. Each transaction applied to the ledger incurs a small fee — which is necessary to prevent bad actors from spamming the network — and the ledger is generally updated every 3-5 seconds.

However, most developers don't interact directly with a Bantu Core node. Rather, the program using a Software Development Kit written in their preferred language, and those SDKs, in turn, interact with Expansion, the Bantu-network API. This three-tiered stack divides responsibilities so each piece of software can focus on a specific purpose. Bantu Core concentrates on transaction submission and consensus; Expansion handles queries and converts network data into a friendly format; SDKs abstract away complexity and offer ergonomic access in a variety of languages.

## Bantu SDKs

SDKs make it easy to craft code and handle network queries and transaction submissions. They're linked to in the [SDK section of the docs](../software-and-sdks/index.md), and each is robust and has its own documentation showing you how to request data and create and submit transactions. When you start developing on Bantu, the first step is usually to find the SDK in your language of choice and familiarize yourself with how it works.

## API: Expansion

[Expansion](../run-api-server/index.md) is a RESTful HTTP API server that provides a straightforward way to submit transactions, check accounts, and subscribe to events. Because it’s HTTP, you can communicate with Expansion using an SDK, but you can also use your web browser or simple command-line tools like cURL. Everything there is to know about Expansion is documented in the [API Reference](../api/introduction/index.md) section of the docs.

At the moment, Expansion requires access to Bantu Core's database to function properly — so every Expansion instance connects to a Bantu Core node — but we are increasing its independence from Bantu Core, and soon developers will be able to deploy the API without having to run their own node.

## Network Backbone: Bantu Core

The Bantu Core software does the hard work of validating and agreeing with other instances of Core on the status of every transaction through the [Bantu Consensus Protocol](../glossary/scp.md) \(SCP\). The ledger, transactions, results, history, and even the messages passed between computers running Bantu Core are encoded using XDR, which is incredibly efficient, but not human readable. Bantu Core nodes make up the network — and running a node is crucial if you want to ensure constant access or contribute to the health and decentralization of the network — but most developers don't work directly with Bantu Core. For more on how to set up a node, consult the [Run a Core Node](../run-core-node/index.md) section.

## The Public Network and the Test Network

There are two different versions of the Bantu network: one for testing and one for real-world deployments. The Bantu Development Foundation provides a free public Expansion instance for each, which you can use to submit transactions or query network data.

* [https://expansion.bantu.network/](https://expansion.bantu.network/) is for interacting with the public network
* [https://expansion-testnet.bantu.network/](https://expansion-testnet.bantu.network/) is for interacting with the testnet

Assets on the testnet don't represent anything in the real world, and when you're developing on the testnet, you can get free test XBN from a tool called Friendbot. On the testnet, you're free to experiment, create, and troubleshoot without risking the loss of funds. It generally upgrades a month before the public network — so if you're using it, you need to keep an eye out for major protocol releases — and unlike the public network — where data persists forever — the testnet gets reset every quarter. Additionally, it has a lower ledger limit than the public network: currently, the testnet tops out at 100 operations/ledger; the public network at 1,000 operations/ledger.

Other than that, the two networks are the same: they consist of Bantu Core nodes, support the Expansion API, and work with Bantu SDKs. Both support the same operations, process transactions in 3-5 seconds, and require the same fees and network minimum. In fact, if you build something on the testnet and decide you're ready to deploy it on the public network, all you need to do is change the [Network Passphrase](../glossary/network-passphrase.md). For more, check out our [guide to best practices for building on the testnet](../glossary/testnet.md).

