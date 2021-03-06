---
title: Expansion API Reference
order: 0
---

# Index

Expansion is an API for interacting with the Bantu network.

This API serves as the bridge between apps and [Bantu Core](../../run-core-node/index.md). Projects like wallets, decentralized exchanges, and asset issuers use Expansion to submit transactions, query an account balance, or stream events like transactions to an account.

Expansion is a [RESTful API](https://en.wikipedia.org/wiki/Representational_state_transfer) and can be accessed via cURL, a browser, or one of the [Bantu SDKs](../../software-and-sdks/index.md). To reduce the complexity of your project, we recommend you use an SDK instead of making direct API calls.

The Bantu Blockchain Foundation \(BBF\) runs two instances of Expansion:

* [https://Expansion.Bantu.org/](https://Expansion.Bantu.network/) for interacting with the public network
* [https://Expansion-testnet.Bantu.org/](https://Expansion-testnet.Bantu.network/) for interacting with the [testnet](../../glossary/testnet.md)

API Reference Sections

| [Introduction](./) | How Expansion is structured. |
| :--- | :--- |
| [Resources](../resources/) | Descriptions of resources and their endpoints. |
| [Aggregations](../aggregations/) | Descriptions of specialized endpoints. |
| [Errors](../errors/) | Potential errors and what they mean. |



