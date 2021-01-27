---
title: Issue an Asset
order: 20
---

# Issue an Asset

There is no dedicated operation to create an asset on Bantu. Instead, assets are created with a [payment operation](../start/list-of-operations.md#payment): an issuing account makes a payment using the asset it’s issuing, and that payment actually creates the asset on the network.

It’s a pretty simple process that requires four operations: one to create an issuing account, one to create a distribution account, one to establish a trustline, and one to make a payment.

Note: you don't actually have to issue assets to a dedicated distribution account: you can issue them to any account with the requisite trustline. However, using a distribution account is the recommended practice, and it makes the process a lot easier to explain. So that's how we'll do it in this guide.

The code to create those operations and submit them as transactions is below. Here, we’ll walk through each step so that the process makes sense. You can breeze through to get a general understanding, or you can use the [Bantu laboratory](https://laboratory.bantu.network/), which is an interface that allows you to create and submit transactions, to actually follow along and issue a token right here right now.

One caveat: if you are creating a token on the public network, there is an additional prerequisite. You need a funded account to provide the XLM necessary to create the issuing and distribution accounts.

## Create the Issuing and Distribution Accounts

The issuing account is the origin of the asset, and will be forever linked to the asset’s identity. The distribution account is the first recipient of the asset. In the final step of this process, you’ll create the asset by sending a payment from the issuing account to the distribution account.

There are two steps to account creation:

1. Generate a keypair
2. Fund the account using a `create_account` operation

You can generate a keypair for free, but an account doesn’t exist on the Bantu ledger until it is funded with XLM to cover the minimum balance.

If you’re issuing an asset on the testnet, you can fund your accounts by getting free test XLM from Friendbot. If you’re issuing an asset in production, you will need to use an existing account to send enough live XLM to cover the minimum balance, transaction fees, and, in the case of the distribution account, a trustline.

Rule of thumb for production: don’t skirt too close to the minimum network balance. If you do, you may not have enough XLM to do what you need to do. Since the network minimum balance and transaction fees are low, it doesn’t require much to get started. 5 XLM should be sufficient. 100 XLM is even better.

### Why Have Separate Accounts for Issuing and Distribution?

Distributing assets through a distribution account is a design pattern. Functionally, you can do away with the distribution account and distribute directly from the issuer account. A less-known fact is that you can even create a market directly from the issuing account and issue by trading.

With that said, there are two main reasons to use a distribution account:

1. Security
2. Auditing

The account you use to distribute your asset from is going to be a _hot_ account, meaning that some web service out there has direct access to sign its transactions.

If the account you use to distribute your asset _is also the issuing account_ and is compromised by a malicious actor, _that actor can now issue as much of your asset as they want_. This is a hostile takeover of the asset and can increase your potential off-chain liabilities. If the malicous actor redeems these newly issued tokens with the anchor service, the anchor may not have the liquidity to support customers' withdrawals.

If the account you use to distribute your asset _is not the issuing account_, then the stakes are lower. Once discovered, the issuer account can effectively freeze the compromised account's asset balance and start fresh with a new distribution account. This is possible without changing the issuing account.

The second reason is bookkeeping or auditability. The issuing account can't actually hold a balance of its own asset. If you have standing inventory of your own asset in a separate account, it is easier to track. This is a common pattern in various ledgering solutions.

As an added bonus, distribution accounts decouple our ecosystem standards from issuance. This allows ecosystem participants to come up with interesting concepts like non-issuing anchors _without_ actually changing protocols.

## Create a Trustline

Bantu requires accounts to explicitly opt-in to holding an asset by creating a trustline, and in this step the distribution account submits a `change_trust` operation to do just that. The trustline goes from the distribution account to the issuing account.

The distribution account specifies the issuer’s public key and the asset code in the `change_trust` operation, and since it’s the first time the asset code appears on the ledger, that means the _distribution_ account actually names the asset, not the issuing account.

Currently, there are two supported formats for asset codes.

* **Alphanumeric 4-character maximum**: Any characters from the set \[a-z\]\[a-z\]\[0-9\] are allowed. The code can be shorter than 4 characters, but the trailing characters must all be empty.
* **Alphanumeric 12-character maximum**: Any characters from the set \[a-z\]\[a-z\]\[0-9\] are allowed. The code can be any number of characters from 5 to 12, but the trailing characters must all be empty.

Any asset code works provided it falls into one of those two buckets. That said, if you’re issuing a currency, you should use the appropriate [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) code, and if you’re issuing a stock or bond, the appropriate [ISIN number](https://en.wikipedia.org/wiki/International_Securities_Identification_Number). Doing so makes it easier for Bantu interfaces to properly display and sort your token in their listings, and allows potential token holders to understand, at a glance, what your token represents.

## Make a Payment

This is the step where the magic happens. The issuing account makes a payment to the distribution account using the newly named asset, and tokens exist where before there were none. Presto!

As long as the issuing account remains unlocked, it can continue to create new tokens by making payments to the distribution account, or to any other account with the requisite trustline.

If you’re planning to do, really, anything with your asset, your next step is to [complete a Bantu.toml file](publishing-asset-info.md) to provide wallets, exchanges, market listing services, and potential token holders with the information they need to understand what it represents.

Once you’ve done that, you can also [create a sell offer](https://github.com/slideloft/new-docs/tree/046158a008b14dc6d54bdd6f4c48e078c303a05e/content/docs/issuing-assets/list-asset-on-dex.mdx) to get your asset onto the Bantu decentralized exchange, and put some effort into market making to create liquidity for it.

## Sample Code

```javascript
var BantuSdk = require("Bantu-sdk");
var server = new BantuSdk.Server("https://expansion-testnet.bantu.network");

// Keys for accounts to issue and receive the new asset
var issuingKeys = BantuSdk.Keypair.fromSecret(
  "SCZANGBA5YHTNYVVV4C3U252E2B6P6F5T3U6MM63WBSBZATAQI3EBTQ4",
);
var receivingKeys = BantuSdk.Keypair.fromSecret(
  "SDSAVCRE5JRAI7UFAVLE5IMIZRD6N6WOJUWKY4GFN34LOBEEUS4W2T2D",
);

// Create an object to represent the new asset
var astroDollar = new BantuSdk.Asset("AstroDollar", issuingKeys.publicKey());

// First, the receiving account must trust the asset
server
  .loadAccount(receivingKeys.publicKey())
  .then(function (receiver) {
    var transaction = new BantuSdk.TransactionBuilder(receiver, {
      fee: 100,
      networkPassphrase: BantuSdk.Networks.TESTNET,
    })
      // The `changeTrust` operation creates (or alters) a trustline
      // The `limit` parameter below is optional
      .addOperation(
        BantuSdk.Operation.changeTrust({
          asset: astroDollar,
          limit: "1000",
        }),
      )
      // setTimeout is required for a transaction
      .setTimeout(100)
      .build();
    transaction.sign(receivingKeys);
    return server.submitTransaction(transaction);
  })
  .then(console.log)

  // Second, the issuing account actually sends a payment using the asset
  .then(function () {
    return server.loadAccount(issuingKeys.publicKey());
  })
  .then(function (issuer) {
    var transaction = new BantuSdk.TransactionBuilder(issuer, {
      fee: 100,
      networkPassphrase: BantuSdk.Networks.TESTNET,
    })
      .addOperation(
        BantuSdk.Operation.payment({
          destination: receivingKeys.publicKey(),
          asset: astroDollar,
          amount: "10",
        }),
      )
      // setTimeout is required for a transaction
      .setTimeout(100)
      .build();
    transaction.sign(issuingKeys);
    return server.submitTransaction(transaction);
  })
  .then(console.log)
  .catch(function (error) {
    console.error("Error!", error);
  });
```

Naturally, the balances for the distributor's account will now hold both XLM and our new Astrodollars.

