---
title: Send and Receive Payments
order: 20
---

# Send and Receive Payments

Most of the time, you’ll be sending money to someone else who has their own account. For this tutorial, however, you'll need a second account to transact with. So before proceeding, follow the steps outlined in [Create an Account](create-account.md) to make _two_ accounts: one for sending and one for receiving.

## About Operations and Transactions

Actions that do things on Bantu— like sending payments or making buy or sell offers — are called [operations](../glossary/operations.md). To submit an operation to the network, you bundle it into a [transaction](../glossary/transactions.md), which is a group of anywhere from 1 to 100 operations accompanied by some extra information, like which account is making the transaction and a cryptographic signature to verify that the transaction is authentic.

Transactions are atomic, meaning that if any operation in a transaction fails, they all fail. Let’s say you have 100 XBN and you make two payment operations of 60 XBN each. If you make two transactions \(each with one operation\), the first will succeed and the second will fail because you don’t have enough XBN. You’ll be left with 40 XBN. However, if you group the two payments into a single transaction, they will both fail and you’ll be left with the full 100 XBN still in your account.

Every transaction also incurs a small fee. Like the minimum balance on accounts, this fee deters spam and prevents people from overloading the system. This [base fee](../glossary/fees.md) is very small — 100 spirits per operation where a stroop equals 1 \* 10 ^-7 XBN — and it's charged for each operation in a transaction. A transaction with two operations, for instance, would cost 200 spirits.

## Send a Payment

Bantustores and communicates transaction data in a binary format called [XDR](../glossary/xdr.md), which is optimized for network performance but unreadable to the human eye. Luckily, [Expansion](../api/introduction/index.md), the BantuAPI, and the [BantuSDKs](../software-and-sdks/index.md) convert XDRs into friendlier formats. Here’s how you might send 10 XBN to an account:

```text
var StellarSdk = require("stellar-sdk");
var server = new StellarSdk.Server("https://expansion-testnet.bantu.network");
var sourceKeys = StellarSdk.Keypair.fromSecret(
  "SCZANGBA5YHTNYVVV4C3U252E2B6P6F5T3U6MM63WBSBZATAQI3EBTQ4",
);
var destinationId = "GA2C5RFPE6GCKMY3US5PAB6UZLKIGSPIUKSLRB6Q723BM2OARMDUYEJ5";
// Transaction will hold a built transaction we can resubmit if the result is unknown.
var transaction;

// First, check to make sure that the destination account exists.
// You could skip this, but if the account does not exist, you will be charged
// the transaction fee when the transaction fails.
server
  .loadAccount(destinationId)
  // If the account is not found, surface a nicer error message for logging.
  .catch(function (error) {
    if (error instanceof StellarSdk.NotFoundError) {
      throw new Error("The destination account does not exist!");
    } else return error;
  })
  // If there was no error, load up-to-date information on your account.
  .then(function () {
    return server.loadAccount(sourceKeys.publicKey());
  })
  .then(function (sourceAccount) {
    // Start building the transaction.
    transaction = new StellarSdk.TransactionBuilder(sourceAccount, {
      fee: StellarSdk.BASE_FEE,
      networkPassphrase: StellarSdk.Networks.TESTNET,
    })
      .addOperation(
        StellarSdk.Operation.payment({
          destination: destinationId,
          // Because Bantu allows transaction in many currencies, you must
          // specify the asset type. The special "native" asset represents Lumens.
          asset: StellarSdk.Asset.native(),
          amount: "10",
        }),
      )
      // A memo allows you to add your own metadata to a transaction. It's
      // optional and does not affect how Bantu treats the transaction.
      .addMemo(StellarSdk.Memo.text("Test Transaction"))
      // Wait a maximum of three minutes for the transaction
      .setTimeout(180)
      .build();
    // Sign the transaction to prove you are actually the person sending it.
    transaction.sign(sourceKeys);
    // And finally, send it off to Bantu!
    return server.submitTransaction(transaction);
  })
  .then(function (result) {
    console.log("Success! Results:", result);
  })
  .catch(function (error) {
    console.error("Something went wrong!", error);
    // If the result is unknown (no response body, timeout etc.) we simply resubmit
    // already built transaction:
    // server.submitTransaction(transaction);
  });
```

What exactly happened there? Let’s break it down.

Confirm that the account ID \(aka the _public key_\) you are sending to actually exists by loading the associated account data from the Bantu network. It's okay to skip this step, but it gives you an opportunity to avoid making a transaction that will inevitably fail.

```text
server.loadAccount(destinationId).then(function (account) {
  /* validate the account */
});
```

Load data for the account you are sending from. An account can only perform one transaction at a time and has something called a [sequence number](../glossary/accounts.md#sequence-number), which helps Bantu verify the order of transactions. A transaction’s sequence number needs to match the account’s sequence number, so you need to get the account’s current sequence number from the network.

```text
.then(function() {
return server.loadAccount(sourceKeys.publicKey());
})
```

The SDK will automatically increment the account’s sequence number when you build a transaction, so you won’t need to retrieve this information again if you want to perform a second transaction.

Start building a transaction. This requires an account object, not just an account ID, because it will increment the account’s sequence number.

```text
var transaction = new StellarSdk.TransactionBuilder(sourceAccount);
```

Add the payment operation to the account. Note that you need to specify the type of asset you are sending: Stellar’s network currency is the [XBN](https://www.stellar.org/XBN), but you can send any asset issued on the network. We'll cover sending non-XBN assets [below](send-and-receive-payments.md#transacting-in-other-currencies). For now, though, we’ll stick to XBN, which are called “native” assets in the SDK:

```text
.addOperation(StellarSdk.Operation.payment({
  destination: destinationId,
  asset: StellarSdk.Asset.native(),
  amount: "10"
}))
```

You should also note that the amount is a string rather than a number. When working with extremely small fractions or large values, [floating point math can introduce small inaccuracies](https://en.wikipedia.org/wiki/Floating_point#Accuracy_problems). Since not all systems have a native way to accurately represent extremely small or large decimals, Bantu uses strings as a reliable way to represent the exact amount across any system.

Optionally, you can add your own metadata, called a [memo](../glossary/transactions.md#memo), to a transaction. Bantu doesn’t do anything with this data, but you can use it for any purpose you’d like. Many exchanges require memos for incoming transactions because they use a single Bantu account for all their users and rely on the memo to differentiate between internal user accounts.

```text
.addMemo(StellarSdk.Memo.text('Test Transaction'))
```

Now that the transaction has all the data it needs, you have to cryptographically sign it using your secret key. This proves that the data actually came from you and not someone impersonating you.

```text
transaction.sign(sourceKeys);
```

And finally, submit it to the Bantu network!

```text
server.submitTransaction(transaction);
```

In this example, we're submitting the transaction to the Bantu-maintained public testnet instance of Expansion, the BantuAPI. When submitting transactions to an Expansion server — which is what most people do — it's possible that you will not receive a response from the server due to a bug, network conditions, etc. In such a situation it's impossible to determine the status of your transaction. That's why you should always save a built transaction \(or transaction encoded in XDR format\) in a variable or a database and resubmit it if you don't know its status. If the transaction has already been successfully applied to the ledger, Expansion will simply return the saved result and not attempt to submit the transaction again. Only in cases where a transaction’s status is unknown \(and thus will have a chance of being included into a ledger\) will a resubmission to the network occur.

## Receive a Payment

You don’t actually need to do anything to receive payments into a Bantu account: if a payer makes a successful transaction to send assets to you, those assets will automatically be added to your account.

However, you may want to keep an eye out for incoming payments. A simple program that watches the network for payments and prints each one might look like:

```text
var StellarSdk = require("stellar-sdk");

var server = new StellarSdk.Server("https://horizon-testnet.stellar.org");
var accountId = "GC2BKLYOOYPDEFJKLKY6FNNRQMGFLVHJKQRGNSSRRGSMPGF32LHCQVGF";

// Create an API call to query payments involving the account.
var payments = server.payments().forAccount(accountId);

// If some payments have already been handled, start the results from the
// last seen payment. (See below in `handlePayment` where it gets saved.)
var lastToken = loadLastPagingToken();
if (lastToken) {
  payments.cursor(lastToken);
}

// `stream` will send each recorded payment, one by one, then keep the
// connection open and continue to send you new payments as they occur.
payments.stream({
  onmessage: function (payment) {
    // Record the paging token so we can start from here next time.
    savePagingToken(payment.paging_token);

    // The payments stream includes both sent and received payments. We only
    // want to process received payments here.
    if (payment.to !== accountId) {
      return;
    }

    // In Stellar’s API, Lumens are referred to as the “native” type. Other
    // asset types have more detailed information.
    var asset;
    if (payment.asset_type === "native") {
      asset = "lumens";
    } else {
      asset = payment.asset_code + ":" + payment.asset_issuer;
    }

    console.log(payment.amount + " " + asset + " from " + payment.from);
  },

  onerror: function (error) {
    console.error("Error in payment stream");
  },
});

function savePagingToken(token) {
  // In most cases, you should save this to a local database or file so that
  // you can load it next time you stream new payments.
}

function loadLastPagingToken() {
  // Get the last paging token from a local database or file
}
```

There are two main parts to this program. First, you create a query for payments involving a given account. Like most queries in Bantu, this could return a huge number of items, so the API returns paging tokens, which you can use later to start your query from the same point where you previously left off. In the example above, the functions to save and load paging tokens are left blank, but in a real application, you’d want to save the paging tokens to a file or database so you can pick up where you left off in case the program crashes or the user closes it.

```text
var payments = server.payments().forAccount(accountId);
var lastToken = loadLastPagingToken();
if (lastToken) {
  payments.cursor(lastToken);
}
```

Second, the results of the query are streamed. This is the easiest way to watch for payments or other transactions. Each existing payment is sent through the stream, one by one. Once all existing payments have been sent, the stream stays open and new payments are sent as they are made.

Try it out: Run this program, and then, in another window, create and submit a payment. You should see this program log the payment.

```text
payments.stream({
  onmessage: function (payment) {
    // handle a payment
  },
});
```

You can also request payments in groups or pages. Once you’ve processed each page of payments, you’ll need to request the next one until there are none left.

```text
payments.call().then(function handlePage(paymentsPage) {
  paymentsPage.records.forEach(function (payment) {
    // handle a payment
  });
  return paymentsPage.next().then(handlePage);
});
```

## Transacting in Other Currencies

One of the amazing things about the Bantu network is that you can create, hold, send, receive, and trade any type of asset. Many organizations issue assets on Bantu that represent real-world currencies such as US dollars or Nigerian naira or other cryptocurrencies such as bitcoin or ether.

Each of these redeemable assets — _anchored_ in the Bantu vernacular — is essentially a credit issued by a particular account that represents reserves those accounts hold outside the network. That's why the assets in the example above had both a `code` and an `issuer`: the `issuer` is the public key of the account that created the asset, an account owned by the organization that ultimately honors the credit that asset represents. To find out more about how that works, check out [Enable Deposits and Withdrawals](../anchoring-assets/enabling-deposit-and-withdrawal/index.md).

