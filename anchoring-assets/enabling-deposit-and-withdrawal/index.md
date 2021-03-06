---
title: 'SEP-24: Deposits & Withdrawals'
order: 10
---

# index

Supporting deposits and withdrawals of an asset on and off the Stellar network requires cooperation between wallet \(client\) and anchor \(server\) applications. In this section, we'll only go over the steps necessary for building a SEP-24 server, but we also have documentation for [building a wallet](../../building-apps/index.md).

Specifically, we will go over SDF's [Tools and References](reference-implementations.md) as well as all three stages of the development process:

1. [Setting up a test server](setting-up-test-server.md)
2. [Setting up a production server](setting-up-production-server.md)
3. [Launching](launch.md)

## The Basic User Experience

The complete customer experience from deposit to withdrawal goes something like this:

1. The customer opens the SEP-24 wallet application of their choice
2. The customer selects an asset to deposit and the wallet finds an anchor \(clients could also chose the specific anchor\)
3. Once the wallet authenticates with the anchor, the customer begins entering their KYC and transaction information requested by the anchor
4. The wallet provides instructions, and the customer deposits real fiat currency with the anchor \(e.g. makes a bank transfer\)
5. Once the wallet receives the deposit, the customer receives the tokenized asset on the Stellar network from the anchor's distribution account

The customer can then use the digital asset on the Stellar network for remittance, payments, trading, store of value, or another use case not listed here. At some later date, the customer could decide to withdraw their assets from the Stellar network, which would look something like this:

1. The customer opens their wallet application
2. The customer selects the asset for withdrawal and wallet finds the anchor
3. After authenticating with the anchor, the wallet opens the given interactive URL and allows the customer to enter their transaction information \(KYC has already been collected\)
4. After asking for customer approval, the wallet sends the specified amount of the customer's asset balance to the anchor's distribution account on Stellar
5. Once the anchor receives the payment, the customer receives the withdrawn funds via bank transfer.

## Interoperability and Stellar Ecosystem Proposals

As already mentioned, this guide will focus on the **Interactive Anchor/Wallet Asset Transfer** SEP \(aka [SEP-24](https://github.com/stellar/stellar-protocol/blob/master/ecosystem/sep-0024.md)\), but SEP-24 requires [SEP-1](https://github.com/stellar/stellar-protocol/blob/master/ecosystem/sep-0001.md), which links meta-information to organizations and assets \(which we go over in detail with [this guide](../../issuing-assets/publishing-asset-info.md)\), and [SEP-10](https://github.com/stellar/stellar-protocol/blob/master/ecosystem/sep-0010.md), which creates authenticated user session.

