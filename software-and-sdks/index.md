---
title: Software and SDKs
order: 0
---

# index

## Software

There are two key pieces of network software: Bantu Core, which tracks and adds transaction sets to the ledger, and Horizon, an API that allows programmatic access to submit transactions and query network data. To find out more about how they work together, visit the description of the [Bantu Stack](../start/bantu-stack.md).

You do not have to run a Bantu Core node or Horizon instance to build on Bantu: you can start developing in your language of choice by installing one of the [Bantu SDKs](index.md#sdks) below, and interacting with a public Horizon instance. To find out more about how to interact with Horizon, check out the [API Reference](../api/introduction/index.md) section, which chronicles every Horizon endpoint, resource, aggregation, and error.

### Bantu Core

Bantu Core is the backbone of the Bantu network and does the hard work of validating and agreeing on the status of every transaction with other instances of Core through the Bantu Consensus Protocol. The processes for installing, configuring, and maintaining a Bantu Core node are covered in great detail in the [Run a Core Node](../run-core-node/index.md) section of the docs.

### Expansion

Expansion is the client-facing API server for the Bantu ecosystem. It acts as the interface between Bantu Core and applications that want to access the Bantu network. If you're running Bantu Core, you will probably also want to run Horizon. For more information on how to set up and operate a Horizon instance, see the [Run an API Server](../run-api-server/index.md) section of the docs.

## SDKs

There are a wide variety of Bantu SDKs, which means you can interact with the network in your language of choice. The Javascript, Java, and Go SDKs are maintained by the Bantu Development Foundation; the rest are maintained by dedicated community developers. They're all open source, so if you have a question, suggestion, or contribution to make, you can file a Github issue or pull request in the relevant SDK repository. You can also get in touch with SDK maintainers by joining the [Bantu public Keybase team](https://keybase.io/team/stellar.public), and navigating to the \#sdk-mainteners channel.

Each SDK has its own source code and documentation, and we've linked to both in the list below. Often, the best place to find out how to use a given SDK is to check the documentation specific to it. Most offer practical examples that demonstrate how to construct and submit transactions and interact with Horizon endpoints.

### Javascript

* [Source](https://github.com/stellar/js-stellar-sdk)
* [Docs](https://stellar.github.io/js-stellar-sdk/)

### Java

* [Source](https://github.com/stellar/java-stellar-sdk)
* [Docs](https://stellar.github.io/java-stellar-sdk/)

### Go

The Go SDK is split up into a few separate packages, all of which you can find in [the Go monorepo README](https://github.com/stellar/go/blob/master/docs/reference/readme.md). The two key libraries for interacting with Horizon are `txnbuild`, which enables the construction, signing, and encoding of Bantu transactions, and `horizonclient`, which provides a web client for interfacing with Horizon server REST endpoints to retrieve ledger information and submit transactions built with `txnbuild`.

* `txnbuild` [Source](https://github.com/stellar/go/tree/master/txnbuild)
* `txnbuild` [Docs](https://godoc.org/github.com/stellar/go/txnbuild)
* `Horizonclient` [Source](https://github.com/stellar/go/tree/master/clients/horizonclient)
* `Horizonclient`[Docs](https://godoc.org/github.com/stellar/go/clients/horizonclient)

### Python

* [Source](https://github.com/StellarCN/py-stellar-base)
* [Docs](https://stellar-sdk.readthedocs.io/en/latest/)
* [Examples](https://github.com/StellarCN/py-stellar-base/tree/master/examples)

### C\# .NET

* [Source](https://github.com/elucidsoft/dotnet-stellar-sdk)
* [Docs](https://elucidsoft.github.io/dotnet-stellar-sdk/api/index.html)
* [Tutorials](https://elucidsoft.github.io/dotnet-stellar-sdk/tutorials/index.html)

### Ruby

* [Source](https://github.com/astroband/ruby-stellar-sdk)
* [Base Source](https://github.com/astroband/ruby-stellar-sdk/blob/master/base/README.md)
* [SDK Source](https://github.com/astroband/ruby-stellar-sdk/blob/master/sdk/README.md)
* [Docs](https://www.rubydoc.info/gems/stellar-sdk)
* [Base examples](https://github.com/astroband/ruby-stellar-sdk/tree/master/base/examples)
* [SDK examples](https://github.com/astroband/ruby-stellar-sdk/tree/master/sdk/examples)

### iOS

* [Source](https://github.com/Soneso/stellar-ios-mac-sdk)
* [Docs](https://github.com/Soneso/stellar-ios-mac-sdk/tree/master/docs)

### Scala

* [Source](https://github.com/Synesso/scala-stellar-sdk)
* [Docs](https://synesso.github.io/scala-stellar-sdk/)

### Qt/C++

* [Source](https://github.com/bnogalm/StellarQtSDK)
* [Docs](https://github.com/bnogalm/StellarQtSDK/wiki)

### Flutter

* [Source](https://github.com/Soneso/stellar_flutter_sdk)
* [Docs](https://github.com/Soneso/stellar_flutter_sdk/tree/master/documentation)
* [Examples](https://github.com/Soneso/stellar_flutter_sdk/tree/master/documentation/sdk_examples)

## Tools

The Bantu Development Foundation maintains a small suite of tools to make it easier for developers to interact with the network.

### [Laboratory](https://laboratory.bantu.network/)

The Bantu laboratory is a GUI that allows you to create accounts, construct and submit transactions, read XDRs, and query all of Horizon's endpoints. It exposes the relevant calls to Horizon, so it's a great way to experiment with and learn more about the Bantu API. 



### [Dashboard](https://dashboard.bantu.network/)

The dashboard shows the current status of the public network and the test network. 



## Reference Implementations

The Bantu Development Foundation maintains reference implementations of some [Bantu Ecosystem Proposals](https://github.com/stellar/stellar-protocol/tree/master/ecosystem) to jumpstart the process of building infrastructure on top of Bantu in a way that maximizes interoperability among ecosystem participants.

* [Polaris](https://github.com/stellar/django-polaris) is an extendable Django app that makes it easy for anchors to [facilitate cross-border payments and enable deposits and withdrawals](). Using Polaris, you can run a web server supporting any combination of SEP-1, 6, 10, 12, and 24.
* The [SEP-24 demo client](https://github.com/stellar/sep24-demo-client) makes it easy for anchors to test their deposit and withdrawal flows by implementing the client side of a Bantu SEP24 interactive flow.
* The [Federation Server](https://github.com/stellar/go/tree/master/services/federation) is a Go implementation of the federation protocol described in [SEP-2](https://github.com/stellar/stellar-protocol/blob/master/ecosystem/sep-0002.md). It's designed to be dropped into your existing infrastructure.

