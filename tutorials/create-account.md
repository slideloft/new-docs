---
title: Create an Account
order: 10
---

# Create Account



Before we get started with working with Bantu in code, consider going through the following examples using the [Bantu Laboratory](https://laboratory.bantu.network/). The lab allows you create accounts, fund accounts on the Bantu test network, build transactions, run any operation, and inspect responses from Expansion via the Endpoint Explorer. 

Accounts are a fundamental building block of Bantu: they hold all your balances, allow you to send and receive payments, and let you place offers to buy and sell assets. Since pretty much everything on Bantu is in some way tied to an account, the first thing you generally need to do when you start developing is create one. This beginner-level tutorial will show you how to do that.

## Create a Keypair

Bantu uses public key cryptography to ensure that every transaction is secure: every Bantu account has a keypair consisting of a public key and a secret key. The public key is always safe to share — other people need it to identify your account and verify that you authorized a transaction. It's like an email address. The secret key, however, is private information that proves you own — and gives you access to — your account. It's like a password, and you should never share it with anyone.

Before creating an account, you need to generate your own keypair:

```text
const pair = StellarSdk.Keypair.random();

pair.secret();
// SAV76USXIJOBMEQXPANUOQM6F5LIOTLPDIDVRJBFFE2MDJXG24TAPUU7
pair.publicKey();
// GCFXHS4GXL6BVUCXBWXGTITROWLVYXQKQLF4YH5O5JT3YZXCYPAFBJZB
```

## Create Account

A valid keypair, however, does not an account make: in order to prevent unused accounts from bloating the ledger, Bantu requires accounts to hold a [minumum balance](../glossary/minimum-balance.md) of 1 XBN before they actually exist. Until it gets a bit of funding, your keypair doesn't warrant space on the ledger.

On the [public network](../glossary/network-passphrase.md), where live users make live transactions, your next step would be to acquire XBN. Because this tutorial runs on the [test network](../glossary/testnet.md), you can get 10,000 test XLM from Friendbot, which is a friendly account funding tool.

To do that, send Friendbot the public key you created. It’ll create and fund a new account using that public key as the account ID.

```text
// The SDK does not have tools for creating test accounts, so you'll have to
// make your own HTTP request.

// if you're trying this on Node, install the `node-fetch` library and
// uncomment the next line:
// const fetch = require('node-fetch');

(async function main() {
  try {
    const response = await fetch(
      `https://friendbot.dev.bantu.network?addr=${encodeURIComponent(
        pair.publicKey(),
      )}`,
    );
    const responseJSON = await response.json();
    console.log("SUCCESS! You have a new account :)\n", responseJSON);
  } catch (e) {
    console.error("ERROR!", e);
  }
})();
```

Now for the last step: getting the account’s details and checking its balance. Accounts can carry multiple balances — one for each type of currency they hold.

 \`\`\`js const server = new StellarSdk.Server\("https://horizon-testnet.stellar.org"\); // the JS SDK uses promises for most actions, such as retrieving an account const account = await server.loadAccount\(pair.publicKey\(\)\); console.log\("Balances for account: " + pair.publicKey\(\)\); account.balances.forEach\(function \(balance\) { console.log\("Type:", balance.asset\_type, ", Balance:", balance.balance\); }\); \`\`\` \`\`\`java import org.stellar.sdk.Server; import org.stellar.sdk.responses.AccountResponse; Server server = new Server\("https://horizon-testnet.stellar.org"\); AccountResponse account = server.accounts\(\).account\(pair.getAccountId\(\)\); System.out.println\("Balances for account " + pair.getAccountId\(\)\); for \(AccountResponse.Balance balance : account.getBalances\(\)\) { System.out.printf\( "Type: %s, Code: %s, Balance: %s%n", balance.getAssetType\(\), balance.getAssetCode\(\), balance.getBalance\(\) \); } \`\`\` \`\`\`go package main import \( "log" "github.com/stellar/go/clients/horizonclient" \) func main\(\) { // Replace this with the output from earlier, or use pair.Address\(\) address := "GCFXHS4GXL6BVUCXBWXGTITROWLVYXQKQLF4YH5O5JT3YZXCYPAFBJZB" request := horizonclient.AccountRequest{AccountID: address} account, err := horizonclient.DefaultTestNetClient.AccountDetail\(request\) if err != nil { log.Fatal\(err\) } log.Println\("Balances for account:", address\) for \_, balance := range account.Balances { log.Println\(balance\) } } \`\`\` \`\`\`python from stellar\_sdk.server import Server server = Server\("https://horizon-testnet.stellar.org"\) public\_key = "GD4NB2FLQAN5JO7PKPGZJMNBDYQXVSNVC7DEIZMOL5WSNSBLEBUTEF5Q" account = server.accounts\(\).account\_id\(public\_key\).call\(\) for balance in account\['balances'\]: print\(f"Type: {balance\['asset\_type'\]}, Balance: {balance\['balance'\]}"\) \`\`\`

Now that you’ve got an account, you can [start sending and receiving payments](send-and-receive-payments.md), or, if you're ready to hunker down, you can skip ahead and [build a wallet](../building-apps/index.md) or [issue a Stellar-network asset](../issuing-assets/index.md).

