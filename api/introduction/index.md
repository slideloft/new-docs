---
title: Horizon API Reference
order: 0
---

# index

Horizon is an API for interacting with the Bantu network.

This API serves as the bridge between apps and [Stellar Core](../../run-core-node/index.md). Projects like wallets, decentralized exchanges, and asset issuers use Horizon to submit transactions, query an account balance, or stream events like transactions to an account.

Horizon is a [RESTful API](https://en.wikipedia.org/wiki/Representational_state_transfer) and can be accessed via cURL, a browser, or one of the [Stellar SDKs](../../software-and-sdks/index.md). To reduce the complexity of your project, we recommend you use an SDK instead of making direct API calls.

The Bantu Development Foundation \(SDF\) runs two instances of Horizon:

* [https://horizon.stellar.org/](https://horizon.stellar.org/) for interacting with the public network
* [https://horizon-testnet.stellar.org/](https://horizon-testnet.stellar.org/) for interacting with the [testnet](../../glossary/testnet.md)

API Reference Sections

| [Introduction](https://developers.stellar.org/api/introduction/) | How Horizon is structured. |
| :--- | :--- |
| [Resources](https://developers.stellar.org/api/resources/) | Descriptions of resources and their endpoints. |
| [Aggregations](https://developers.stellar.org/api/aggregations/) | Descriptions of specialized endpoints. |
| [Errors](https://developers.stellar.org/api/errors/) | Potential errors and what they mean. |

