---
title: Overview
order: 10
---

# index

import { Alert } from "components/Alert";

Supporting cross-border payments of an asset through the Stellar network requires cooperation between a sending anchor \(**SA**\) and receiving anchor \(**RA**\). In this section, we'll only go over the steps necessary for building a SEP-31 receiving anchor, but documentation for building a sending anchor is in development.

Specifically, we will go over the SDF's [Tools and References](reference-implementations.md) as well as all three stages of the development process:

1. [Setting up a test server](setting-up-test-server.md)
2. [Setting up a production server](setting-up-production-server.md)
3. [Launching](launch.md)

## The Basic User Experience

Unlike with SEP-24, SEP-31 involves a sending user \(**SU**\) and receiving user \(**RU**\), so both users' experience is described here.

 Note: \*\*SA\*\*'s are not necessarily wallet applications. This means the \*\*SU\*\* may not interact with a mobile application, but could go to a website or physical remittance location instead. Obviously, this affects the \*\*SU\*\* experience.

Generally, the experience of the SU and RU would look something like this:

1. The **SU** opens an app, website, or goes to a physical remittance location
2. The **SU** specifies the asset and amount to send, and the asset that should be received
3. The **SA** finds the appropriate **RA** for the asset, authenticates with the **RA**, and parses the **RA**'s requirements for sending payments
4. The **SA** collects both the **SU** and **RU** KYC information requested by the **RA** from the **SU**, as well as the transaction information
   * **RU**'s should not have to take any action to receive a cross-border payment
   * However, it is possible to require action from the **RU** if absolutely necessary
5. The **SA** registers the **RU** and potentially **SU** with the **RA** via [SEP-12](https://github.com/stellar/stellar-protocol/blob/master/ecosystem/sep-0012.md)
6. Once the **RA** is ready to receive the payment, the **SA** makes the Stellar path payment to the **RA** using the **SU** and **RU** assets
7. Once the **RA** receives the path payment, it attempts make the associated off-chain transfer \(usually bank transfer\) using the KYC and transaction information sent by the **SA**
8. If the transfer to the **RU** fails, the **SU** will be notified by the **SA** to update the invalid or missing fields, and the **RA** will retry once the **SA** sends the updated info.

The **RU** should then receive the funds sent by the **SA** once the **RA** has the necessary to make the final transfer.

 Note: The final off-chain transfer by the \*\*RA\*\* may not be a bank transfer. For example, the destination could be a mobile money account managed by the \*\*RA\*\*. The methods used to transfer the payment off-chain to the \*\*RU\*\* is up to the \*\*RA\*\*, and \*\*SA\*\*s should be aware of the off-chain transfer methods of their partner \*\*RA\*\*s.

## Interoperability and Stellar Ecosystem Proposals

As mentioned, this section will outline how to implement a [SEP-31](https://github.com/stellar/stellar-protocol/blob/master/ecosystem/sep-0031.md) receiver, but these servers require [SEP-1](https://github.com/stellar/stellar-protocol/blob/master/ecosystem/sep-0001.md), [10](https://github.com/stellar/stellar-protocol/blob/master/ecosystem/sep-0010.md), and [12](https://github.com/stellar/stellar-protocol/blob/master/ecosystem/sep-0012.md) to be implemented as well. SEP-1 is described in [this guide](../../issuing-assets/publishing-asset-info.md), and SEP-10 & 12 are described here.

