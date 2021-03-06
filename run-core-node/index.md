---
title: Overview
order: 10
---

# index

Bantu is a peer-to-peer network made up of nodes, which are computers that keep a common distributed [ledger](../glossary/ledger.md), and that communicate to validate and add [transactions](../glossary/transactions.md) to it. Nodes use a program called Bantu Core — an implementation of the [Bantu Consensus Protocol](../glossary/scp.md) — to stay in sync as they work to agree on the validity of transaction sets and to apply them to the ledger. Generally, nodes reach consensus, apply a transaction set, and update the ledger every 3-5 seconds.

You don’t need to run a node to build on Bantu: you can start developing with your [SDK of choice](../software-and-sdks/index.md), and use public instances of Horizon to query the ledger and submit transactions right away. In fact, the Bantu Development Foundation offers two public instances of Horizon — one for the public network and one for the testnet — which you can read more about in our [API reference docs](../api/introduction/index.md).

If you’re serious about building on Bantu, have a production-level product or service that requires high-availability access network, or want to help increase network health and decentralization, then you probably _do_ want to run a node, or even a trio of nodes \(more on that in the [Tier 1 section](tier-1-orgs.md)\).

If you’re going the DIY route, this section of the docs is for you. It explains the technical and operational aspects of installing, configuring, and maintaining a Bantu Core node, and should help you figure out the best way to set up your Bantu integration.

The basic flow, which you can navigate through using the menu on the left, goes like this:

* Choose which type of node you want to run
* Prepare Your Environment
* Install Bantu Core
* Configure Bantu Core
* Join the network
* Monitor and maintain your node
* Join the validators channels to stay on top of critical upgrades and network votes

## Types of nodes

All nodes perform the same basic functions: they run Bantu Core, connect to peers, submit transactions, store the state of the ledger in a SQL [database](configuring.md#database), and keep a duplicate copy of the ledger in flat XDR files called [buckets](configuring.md#buckets). All nodes also support [Horizon](../run-api-server/index.md), the Bantu API.

In addition to those basic functions, there are two key configuration options that determine how a node behaves. A node can:

* Participate in consensus to [validate transactions](configuring.md#validating)
* Publish an [archive](publishing-history-archives.md) that other nodes can consult to find the complete history of the network.

To make things easier, we’ll define four types of nodes based on permutations of those two options: **Watcher**, **Basic Validator**, **Full Validator**, and **Archiver**. You’ll notice that they _all_ support Horizon and submit transactions to the network:

| Type of Node | Supports Horizon | Submits Transactions | Validates Transactions | Publishes History |
| :--- | :--- | :--- | :--- | :--- |
| **Watcher** | ✅ | ✅ |  |  |
| **Basic Validator** | ✅ | ✅ | ✅ |  |
| **Full Validator** | ✅ | ✅ | ✅ | ✅ |
| **Archiver** | ✅ | ✅ |  | ✅ |

So why choose one type over another? Let’s break it down a bit and take a look at what each type is good for.

### Watcher

#### Non-validating, no public archive

A Watcher is the lightest node you can run. It keeps track of the ledger and submits transactions for possible inclusion, but it is _not_ configured to participate in validation or to publish a history archive, which means it doesn’t do anything to support the network or increase decentralization.

Watchers pair well with Horizon, and if all you need is a Horizon instance to query the ledger or submit transactions, a Watcher is probably the right choice for you. While there are public instances of Horizon you can use — namely those maintained by [SDF](../api/introduction/index.md), [Lobstr](https://horizon.Bantu.lobstr.co), [Satoshipay](https://Bantu-horizon.satoshipay.io), and [Coinqvest](https://horizon.Bantu.coinqvest.com) — they’re all rate limited, so they won’t work if you need to scale your project or you want to offer your customers an SLA — 99% uptime, for instance.

**Use a Watcher to run Horizon, and to ensure reliable access to the network.**

### Basic Validator

#### Validating, no public archive

A Basic Validator is a lot like a Watcher, and has the same advantages and similar operational requirements. The difference between the two is that a Basic Validator requires a secret key, and is [configured to participate in consensus](configuring.md#validating) by voting on — and signing off on — changes to the ledger.

The advantage: signatures can serve as official endorsements of specific ledgers in real time. That’s important if, for instance, you issue an asset on Bantu that represents a real-world asset: you can let your customers know that you will only honor transactions and redeem assets from ledgers signed by your validator, and in the unlikely scenario that something happens to the network, you can use your node as the final arbiter of truth. Setting up your node as a validator allows you to resolve any questions _up front and in writing_ about how you plan to deal with disasters and disputes.

**Use a Basic Validator to run Horizon, ensure reliable access to the network, and sign off on transactions.**

### Full Validator

#### Validating, offers public archive

A Full Validator is the same as a Basic Validator except that it also publishes a [History Archive](publishing-history-archives.md) containing snapshots of the ledger, including all transactions and their results. A Full Validator writes to an internet-facing blob store — such as AWS or Azure — so it's a bit more expensive and complex to run, but it also does the most to support the network’s resilience and decentralization.

When other nodes join the network — or experience difficulty and temporarily fall out of sync — they can consult archives offered by Full Validators to catch up on the history of the network. Redundant archives prevent a single point of failure, and allow network participants to verify the veracity of a given history.

Full Validators can support Horizon, but generally, organizations that run them don’t use them to query network data or submit transactions. In fact, they often run a Watcher to handle Horizon _in addition_ to Full Validators. Most of those organizations are also part of — or on track to join — [Tier 1](tier-1-orgs.md), which is a core group of network participants who run three Full Validators to contribute maximum redundancy.

**Use a Full Validator to sign off on transactions, and to contribute to the health and decentralization of the network.**

### Archiver

#### Non-validating, offers public archive

An Archiver is a rare bird: like a Full Validator, it publishes the activity of the network in long-term storage; unlike a Full Validator, it does not participate in consensus.

Archivers help with decentralization a bit by offering redundant accounts of the network’s history, but they don’t vote or sign ledgers, so their usefulness is fairly limited. If you run a Bantu-facing service, like a blockchain explorer, you may want to run one. Otherwise, you’re probably better off choosing one of the other three types.

**Use an archiver if you want to referee the network. Which is unlikely.**

