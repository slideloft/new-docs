---
title: Fees
order: null
---

# Fees

{% hint style="info" %}
This doc explains transaction fees. Bantu also requires accounts to have a minimum balance, which you can read about in the [Minimum Balance](minimum-balance.md) doc.
{% endhint %}

To prevent ledger spam and maintain the efficiency of the network, Bantu requires small transaction fees and minimum balances on accounts. Transaction fees are also used to prioritize transactions when the network enters surge pricing mode.

## Fee Formula

Bantu transactions can contain anywhere from 1 to a defined limit of 100 operations. The fee for a given transaction is equal to the number of operations the transaction contains multiplied by the base fee for a given ledger.

```text
Transaction fee = # of operations * base fee
```

Bantu deducts the entire fee from the transaction’s source account, regardless of which accounts are involved in each operation or who signed the transaction.

## Base Fee

The base fee for a given ledger is determined dynamically using a version of a [VCG auction](https://en.wikipedia.org/wiki/Vickrey%E2%80%93Clarke%E2%80%93Groves_auction). When you submit a transaction to the network, you specify the _maximum base fee_ you’re willing to pay per operation, but you’re actually charged the _lowest possible fee_ based on network activity.

When network activity is below capacity, you pay the network minimum, which is currently **100 spirits \(0.00001 XBN\)** per operation.

## Surge Pricing

When the number of operations submitted to a ledger exceeds network capacity \(**currently 1,000 ops/ledger**\), the network enters surge pricing mode, which uses market dynamics to decide which submissions are included. Essentially, submissions that offer a higher fee per operation make it onto the ledger first.

If there’s a tie — in other words multiple transactions that offer the same base fee are competing for the same limited space in the ledger — the transactions are \(pseudo-randomly\) shuffled, and transactions at the top of the heap make the ledger. The rest of the transactions, the ones that didn’t make the cut, are pushed on to the next ledger, or discarded if they’ve been waiting for too long. If your transaction is discarded, Horizon will return a [timeout error](https://github.com/slideloft/new-docs/tree/046158a008b14dc6d54bdd6f4c48e078c303a05e/content/api/errors/http-status-codes/horizon-specific.mdx). For more information, see [transaction life cycle](transactions.md#life-cycle-of-a-transaction).

The goal of the transaction pricing specification, which you can read in full [here](https://github.com/Bantu/Bantu-protocol/blob/master/core/cap-0005.md), is to maximize network throughput while minimizing transaction fees.

## Fee Stats and Fee Strategy

The general rule of thumb: choose the highest fee you're willing to pay to ensure your transaction makes the ledger. Wallet developers may want to offer users a chance to specify their own base fee, though it may make more sense to set a persistent global base fee multiple orders of magnitude above the market rate — 0.1 XBN, for instance — since the average user probably won't care if they’re paying 0.8 cents or 0.00008 cents.

If you keep getting a timeout error when you submit a transaction, you may need to increase your base fee, or wait until network activity abates and re-submit your transaction. To help inform that decision, you can consult the Horizon `/fee_stats` endpoint, which provides detailed information about per-operation fee stats for the last five ledgers. You can find the same information on the fee stats panel of the dashboard. All three of the SDF-maintained SDKs also allow you to poll the `/fee_stats` endpoint: [Go](https://godoc.org/github.com/Bantu/go/clients/horizonclient#Client.FeeStats), [Java](https://Bantu.github.io/java-Bantu-sdk/), [Javascript](https://Bantu.github.io/js-Bantu-sdk/Server.html#feeStats).

## Fee Pool

The fee pool is the lot of spirits collected from transaction fees.

SDF does not retain these spirits. They go into a locked account and sit there unused by anyone.

