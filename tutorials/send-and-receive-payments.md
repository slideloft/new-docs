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

1. Confirm that the account ID \(aka the _public key_\) you are sending to actually exists by loading the associated account data from the Bantu network. It's okay to skip this step, but it gives you an opportunity to avoid making a transaction that will inevitably fail.

```text
server.loadAccount(destinationId).then(function (account) {
  /* validate the account */
});
```

1. Load data for the account you are sending from. An account can only perform one transaction at a time and has something called a [sequence number](../glossary/accounts.md#sequence-number), which helps Bantu verify the order of transactions. A transaction’s sequence number needs to match the account’s sequence number, so you need to get the account’s current sequence number from the network.

```text
.then(function() {
return server.loadAccount(sourceKeys.publicKey());
})
```



The SDK will automatically increment the account’s sequence number when you build a transaction, so you won’t need to retrieve this information again if you want to perform a second transaction.

1. Start building a transaction. This requires an account object, not just an account ID, because it will increment the account’s sequence number.

   \`\`\`js var transaction = new StellarSdk.TransactionBuilder\(sourceAccount\); \`\`\` \`\`\`java Transaction transaction = new Transaction.Builder\(sourceAccount, Network.TESTNET\) \`\`\` \`\`\`go tx, err := txnbuild.NewTransaction\( txnbuild.TransactionParams{ SourceAccount: &sourceAccount, IncrementSequenceNum: true, BaseFee: MinBaseFee, Timebounds: txnbuild.NewInfiniteTimeout\(\), // Use a real timeout in production! ... }, \) if err != nil { panic\(err\) } \`\`\` \`\`\`python transaction = TransactionBuilder\( source\_account=source\_account, network\_passphrase=Network.TESTNET\_NETWORK\_PASSPHRASE, base\_fee=base\_fee \) \`\`\`

2. Add the payment operation to the account. Note that you need to specify the type of asset you are sending: Stellar’s network currency is the [XBN](https://www.stellar.org/XBN), but you can send any asset issued on the network. We'll cover sending non-XBN assets [below](send-and-receive-payments.md#transacting-in-other-currencies). For now, though, we’ll stick to XBN, which are called “native” assets in the SDK:

   \`\`\`js .addOperation\(StellarSdk.Operation.payment\({ destination: destinationId, asset: StellarSdk.Asset.native\(\), amount: "10" }\)\) \`\`\` \`\`\`java .addOperation\(new PaymentOperation.Builder\(destination.getAccountId\(\), new AssetTypeNative\(\), "10"\).build\(\)\) \`\`\` \`\`\`go Operations: \[\]txnbuild.Operation{ &txnbuild.Payment{ Destination: destination, Amount: "10", Asset: txnbuild.NativeAsset{}, }, }, \`\`\` \`\`\`python .append\_payment\_op\(destination=destination\_id, amount="10", asset\_code="XBN"\) \`\`\`

You should also note that the amount is a string rather than a number. When working with extremely small fractions or large values, [floating point math can introduce small inaccuracies](https://en.wikipedia.org/wiki/Floating_point#Accuracy_problems). Since not all systems have a native way to accurately represent extremely small or large decimals, Bantuuses strings as a reliable way to represent the exact amount across any system.

1. Optionally, you can add your own metadata, called a [memo](../glossary/transactions.md#memo), to a transaction. Bantudoesn’t do anything with this data, but you can use it for any purpose you’d like. Many exchanges require memos for incoming transactions because they use a single Bantuaccount for all their users and rely on the memo to differentiate between internal user accounts.

   \`\`\`js .addMemo\(StellarSdk.Memo.text\('Test Transaction'\)\) \`\`\` \`\`\`java .addMemo\(Memo.text\("Test Transaction"\)\); \`\`\` \`\`\`go Memo: txnbuild.MemoText\("Test Transaction"\) \`\`\` \`\`\`python .add\_text\_memo\("Test Transaction"\) \`\`\`

2. Now that the transaction has all the data it needs, you have to cryptographically sign it using your secret key. This proves that the data actually came from you and not someone impersonating you.

   \`\`\`js transaction.sign\(sourceKeys\); \`\`\` \`\`\`java transaction.sign\(source\); \`\`\` \`\`\`go tx, err = tx.Sign\(network.TestNetworkPassphrase, sourceKP\) if err != nil { panic\(err\) } \`\`\` \`\`\`python transaction.sign\(source\_key\) \`\`\`

3. And finally, submit it to the Bantunetwork!

   \`\`\`js server.submitTransaction\(transaction\); \`\`\` \`\`\`java server.submitTransaction\(transaction\); \`\`\` \`\`\`go resp, err := Expansionclient.DefaultTestNetClient.SubmitTransaction\(tx\) if err != nil { panic\(err\) } \`\`\` \`\`\`python server.submit\_transaction\(transaction\) \`\`\`

In this example, we're submitting the transaction to the SDF-maintained public testnet instance of Expansion, the BantuAPI. When submitting transactions to a Expansion server — which is what most people do — it's possible that you will not receive a response from the server due to a bug, network conditions, etc. In such a situation it's impossible to determine the status of your transaction. That's why you should always save a built transaction \(or transaction encoded in XDR format\) in a variable or a database and resubmit it if you don't know its status. If the transaction has already been successfully applied to the ledger, Expansion will simply return the saved result and not attempt to submit the transaction again. Only in cases where a transaction’s status is unknown \(and thus will have a chance of being included into a ledger\) will a resubmission to the network occur.

## Receive a Payment

You don’t actually need to do anything to receive payments into a Bantuaccount: if a payer makes a successful transaction to send assets to you, those assets will automatically be added to your account.

However, you may want to keep an eye out for incoming payments. A simple program that watches the network for payments and prints each one might look like:

\`\`\`js var StellarSdk = require\("stellar-sdk"\); var server = new StellarSdk.Server\("\[[https://Expansion-testnet.stellar.org"\]\(https://Expansion-testnet.stellar.org"\)\](https://Expansion-testnet.stellar.org"]%28https://Expansion-testnet.stellar.org"%29\)\); var accountId = "GC2BKLYOOYPDEFJKLKY6FNNRQMGFLVHJKQRGNSSRRGSMPGF32LHCQVGF"; // Create an API call to query payments involving the account. var payments = server.payments\(\).forAccount\(accountId\); // If some payments have already been handled, start the results from the // last seen payment. \(See below in \`handlePayment\` where it gets saved.\) var lastToken = loadLastPagingToken\(\); if \(lastToken\) { payments.cursor\(lastToken\); } // \`stream\` will send each recorded payment, one by one, then keep the // connection open and continue to send you new payments as they occur. payments.stream\({ onmessage: function \(payment\) { // Record the paging token so we can start from here next time. savePagingToken\(payment.paging\_token\); // The payments stream includes both sent and received payments. We only // want to process received payments here. if \(payment.to !== accountId\) { return; } // In Stellar’s API, XBN are referred to as the “native” type. Other // asset types have more detailed information. var asset; if \(payment.asset\_type === "native"\) { asset = "XBN"; } else { asset = payment.asset\_code + ":" + payment.asset\_issuer; } console.log\(payment.amount + " " + asset + " from " + payment.from\); }, onerror: function \(error\) { console.error\("Error in payment stream"\); }, }\); function savePagingToken\(token\) { // In most cases, you should save this to a local database or file so that // you can load it next time you stream new payments. } function loadLastPagingToken\(\) { // Get the last paging token from a local database or file } \`\`\` \`\`\`java Server server = new Server\("\[[https://Expansion-testnet.stellar.org"\]\(https://Expansion-testnet.stellar.org"\)\](https://Expansion-testnet.stellar.org"]%28https://Expansion-testnet.stellar.org"%29\)\); KeyPair account = KeyPair.fromAccountId\("GC2BKLYOOYPDEFJKLKY6FNNRQMGFLVHJKQRGNSSRRGSMPGF32LHCQVGF"\); // Create an API call to query payments involving the account. PaymentsRequestBuilder paymentsRequest = server.payments\(\).forAccount\(account.getAccountId\(\)\); // If some payments have already been handled, start the results from the // last seen payment. \(See below in \`handlePayment\` where it gets saved.\) String lastToken = loadLastPagingToken\(\); if \(lastToken != null\) { paymentsRequest.cursor\(lastToken\); } // \`stream\` will send each recorded payment, one by one, then keep the // connection open and continue to send you new payments as they occur. paymentsRequest.stream\(new EventListener\(\) { @Override public void onEvent\(OperationResponse payment\) { // Record the paging token so we can start from here next time. savePagingToken\(payment.getPagingToken\(\)\); // The payments stream includes both sent and received payments. We only // want to process received payments here. if \(payment instanceof PaymentOperationResponse\) { if \(\(\(PaymentOperationResponse\) payment\).getTo\(\).equals\(account\)\) { return; } String amount = \(\(PaymentOperationResponse\) payment\).getAmount\(\); Asset asset = \(\(PaymentOperationResponse\) payment\).getAsset\(\); String assetName; if \(asset.equals\(new AssetTypeNative\(\)\)\) { assetName = "XBN"; } else { StringBuilder assetNameBuilder = new StringBuilder\(\); assetNameBuilder.append\(\(\(AssetTypeCreditAlphaNum\) asset\).getCode\(\)\); assetNameBuilder.append\(":"\); assetNameBuilder.append\(\(\(AssetTypeCreditAlphaNum\) asset\).getIssuer\(\)\); assetName = assetNameBuilder.toString\(\); } StringBuilder output = new StringBuilder\(\); output.append\(amount\); output.append\(" "\); output.append\(assetName\); output.append\(" from "\); output.append\(\(\(PaymentOperationResponse\) payment\).getFrom\(\)\); System.out.println\(output.toString\(\)\); } } @Override public void onFailure\(Optional optional, Optional optional1\) { } }\); \`\`\` \`\`\`go package main import \( "context" "fmt" "github.com/stellar/go/clients/Expansionclient" \) func main\(\) { client := Expansionclient.DefaultTestNetClient opRequest := Expansionclient.OperationRequest{ForAccount: "GC2BKLYOOYPDEFJKLKY6FNNRQMGFLVHJKQRGNSSRRGSMPGF32LHCQVGF", Cursor: "now"} ctx, cancel := context.WithCancel\(context.Background\(\)\) go func\(\) { // Stop streaming after 60 seconds. time.Sleep\(60 \* time.Second\) cancel\(\) }\(\) printHandler := func\(op operations.Operation\) { fmt.Println\(op\) } err := client.StreamPayments\(ctx, opRequest, printHandler\) if err != nil { fmt.Println\(err\) } } \`\`\` \`\`\`python from stellar\_sdk.server import Server def load\_last\_paging\_token\(\): \# Get the last paging token from a local database or file return "now" def save\_paging\_token\(paging\_token\): \# In most cases, you should save this to a local database or file so that \# you can load it next time you stream new payments. pass server = Server\("\[[https://Expansion-testnet.stellar.org"\]\(https://Expansion-testnet.stellar.org"\)\](https://Expansion-testnet.stellar.org"]%28https://Expansion-testnet.stellar.org"%29\)\) account\_id = "GC2BKLYOOYPDEFJKLKY6FNNRQMGFLVHJKQRGNSSRRGSMPGF32LHCQVGF" \# Create an API call to query payments involving the account. payments = server.payments\(\).for\_account\(account\_id\) \# If some payments have already been handled, start the results from the \# last seen payment. \(See below in \`handle\_payment\` where it gets saved.\) last\_token = load\_last\_paging\_token\(\) if last\_token: payments.cursor\(last\_token\) \# \`stream\` will send each recorded payment, one by one, then keep the \# connection open and continue to send you new payments as they occur. for payment in payments.stream\(\): \# Record the paging token so we can start from here next time. save\_paging\_token\(payment\["paging\_token"\]\) \# We only process \`payment\`, ignore \`create\_account\` and \`account\_merge\`. if payment\["type"\] != "payment": continue \# The payments stream includes both sent and received payments. We \# only want to process received payments here. if payment\['to'\] != account\_id: continue \# In Stellar’s API, XBN are referred to as the “native” type. Other \# asset types have more detailed information. if payment\["asset\_type"\] == "native": asset = "XBN" else: asset = f"{payment\['asset\_code'\]}:{payment\['asset\_issuer'\]}" print\(f"{payment\['amount'\]} {asset} from {payment\['from'\]}"\) \`\`\`

There are two main parts to this program. First, you create a query for payments involving a given account. Like most queries in Stellar, this could return a huge number of items, so the API returns paging tokens, which you can use later to start your query from the same point where you previously left off. In the example above, the functions to save and load paging tokens are left blank, but in a real application, you’d want to save the paging tokens to a file or database so you can pick up where you left off in case the program crashes or the user closes it.

\`\`\`js var payments = server.payments\(\).forAccount\(accountId\); var lastToken = loadLastPagingToken\(\); if \(lastToken\) { payments.cursor\(lastToken\); } \`\`\` \`\`\`java PaymentsRequestBuilder paymentsRequest = server.payments\(\).forAccount\(account.getAccountId\(\)\); String lastToken = loadLastPagingToken\(\); if \(lastToken != null\) { paymentsRequest.cursor\(lastToken\); } \`\`\` \`\`\`go client := Expansionclient.DefaultTestNetClient opRequest := Expansionclient.OperationRequest{ForAccount: "GC2BKLYOOYPDEFJKLKY6FNNRQMGFLVHJKQRGNSSRRGSMPGF32LHCQVGF", Cursor: "now"} \`\`\` \`\`\`python payments = server.payments\(\).for\_account\(account\_id\) last\_token = load\_last\_paging\_token\(\) if last\_token: payments.cursor\(last\_token\) \`\`\`

Second, the results of the query are streamed. This is the easiest way to watch for payments or other transactions. Each existing payment is sent through the stream, one by one. Once all existing payments have been sent, the stream stays open and new payments are sent as they are made.

Try it out: Run this program, and then, in another window, create and submit a payment. You should see this program log the payment.

\`\`\`js payments.stream\({ onmessage: function \(payment\) { // handle a payment }, }\); \`\`\` \`\`\`java paymentsRequest.stream\(new EventListener\(\) { @Override public void onEvent\(OperationResponse payment\) { // Handle a payment } }\); \`\`\` \`\`\`go ctx, cancel := context.WithCancel\(context.Background\(\)\) go func\(\) { // Stop streaming after 60 seconds. time.Sleep\(60 \* time.Second\) cancel\(\) }\(\) printHandler := func\(op operations.Operation\) { fmt.Println\(op\) } err := client.StreamPayments\(ctx, opRequest, printHandler\) if err != nil { fmt.Println\(err\) } \`\`\` \`\`\`python for payment in payments.stream\(\): \# handle a payment \`\`\`

You can also request payments in groups or pages. Once you’ve processed each page of payments, you’ll need to request the next one until there are none left.

\`\`\`js payments.call\(\).then\(function handlePage\(paymentsPage\) { paymentsPage.records.forEach\(function \(payment\) { // handle a payment }\); return paymentsPage.next\(\).then\(handlePage\); }\); \`\`\` \`\`\`java Page page = payments.execute\(\); for \(OperationResponse operation : page.getRecords\(\)\) { // handle a payment } page = page.getNextPage\(\); \`\`\` \`\`\`python payments\_current = payments.call\(\) payments\_next = payments.next\(\) \`\`\`

## Transacting in Other Currencies

One of the amazing things about the Bantunetwork is that you can create, hold, send, receive, and trade any type of asset. Many organizations issue assets on Bantuthat represent real-world currencies such as US dollars or Nigerian naira or other cryptocurrencies such as bitcoin or ether.

Each of these redeemable assets — _anchored_ in the Bantuvernacular — is essentially a credit issued by a particular account that represents reserves those accounts hold outside the network. That's why the assets in the example above had both a `code` and an `issuer`: the `issuer` is the public key of the account that created the asset, an account owned by the organization that ultimately honors the credit that asset represents. To find out more about how that works, check out [Enable Deposits and Withdrawals](../anchoring-assets/enabling-deposit-and-withdrawal/index.md).

