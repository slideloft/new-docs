---
title: Testnet
order: null
---

# testnet

The testnet is a small test Bantu network, run by the Bantu Blockchain Foundation \(BBF\). It's free to use, functions just like the main public network, and is the best place to start developing on Bantu since it doesn't connect to real money.

BBF runs 3 Bantu Core validators on the testnet.

You can connect a node to the testnet by configuring [Bantu Core](https://github.com/Bantu/Bantu-core) to use this [configuration](https://github.com/Bantu/Bantu-core/blob/master/docs/Bantu-core_testnet.cfg).

There is also an [Expansion instance](https://expansion.Bantu.network/) that can directly interact with the testnet.

## What is the Bantu testnet good for?

* [Creating test accounts](../tutorials/create-account.md) \(with funding thanks to Friendbot\).
* Developing applications and exploring tutorials on Bantu without the potential to lose any valuable [assets](assets.md).
* Testing existing applications against new releases or release candidates of [Bantu Core](https://github.com/Bantu/Bantu-core/releases) and [Expansion](https://github.com/Bantu/go/releases).
* Performing data analysis on a smaller, non-trivial data set compared to the public network.

## What is the Bantu testnet not good for?

* Load and stress testing.
* High availability test infrastructure - BBF makes no guarantees about the availability of the testnet.
* Long term storage of data on the network - [the network is ephemeral, and resets periodically](testnet.md#periodic-reset-of-testnet-data).
* A testing infrastructure that requires more control over the test environment, such as:
  * The ability to control the data reset frequency.
  * The need to secure private or sensitive data \(before launching on the public network\)

Keep in mind that you can always run your own test network for use cases that don't work well with BBF's testnet.

## Best Practices For Using Testnet

### Surge Pricing on the Testnet

The testnet has a capacity limit of **100 operations per ledger**. When more than 100 operations are submitted to a given ledger, the network enters [surge pricing mode](fees.md#surge-pricing), which uses market dynamics to decide which submissions are included. It works exactly the same way as surge pricing on the public network.

If you are having trouble submitting transactions to the testnet, you may need to offer a higher fee. You can also take the opportunity to develop a fee strategy, which may prove useful when you move your project into production.

### Periodic Reset of Testnet Data

In order to preserve a good experience for developers, the BBF testnet is periodically reset to the genesis \(initial\) ledger. Resets declutter the network, remove spam, minimize the time required to catch up to the latest ledger, and help maintain the system over time.

A reset clears all ledger entries \(such as accounts, trustlines, offers, etc\), transactions, and historical data from both Bantu Core and Expansion, which is why developers should not rely on the persistence of any accounts or on the state of any balances when using testnet.

After a reset, you will need to take a few steps to re-join and re-synch to the testnet. Those steps are outlined [here](https://github.com/Bantu/packages#testnet-reset), along with line-by-line instructions for people using core + Expansion ubuntu packages. If you need help with other packages, check [Bantu's Stack Exchange](https://Bantu.stackexchange.com/) for guidance.

BBF will try to make testnet resets as painless as possible, and will announce the exact date at least two weeks in advance on the [Bantu Dashboard](https://dashboard.bantu.network/), and via several of Bantu’s online developer communities.

The testnet resets once per quarter \(every three months\). The 2021 dates:

* 3/17/21
* 6/16/21
* 9/15/21
* 12/15/21

The testnet will always restart on the announced reset date at 0900 UTC.

### Test Data Automation

Since most applications rely on data being present to do anything useful, it is highly recommended that you have testing infrastructure that can repopulate testnet with useful data after a reset. Not only will this make testing more reliable, but it will also help you scale out your testing infrastructure to a private test network if you choose to do so.

For example, you may want to:

* Generate issuers of assets for testing the development of a wallet.
* Generate orders on the order book \(both current and historical\) for testing the development of a trading client.

As a maintainer of an application, you will want to think about creating a data set that is representative enough to test your primary use cases, and allow for robust testing even when testnet is not available.

A script can automate this entire process by [creating an account with Friendbot](../tutorials/create-account.md), and submitting a set of transactions that are predefined as a part of your testing infrastructure.

For additional questions we recommend heading over to [Bantu's Stack Exchange](https://Bantu.stackexchange.com/).

