---
title: Make XBN Payments
order: 50
---

# Make XBN Payments

 In this tutorial we’re going to modify our \[base wallet app\]\(./basic-wallet.mdx\) to include functionality to send XBN to other Stellar accounts.

[View keystore boilerplate code on GitHub](https://github.com/stellar/stellar-demo-wallet/tree/keystore)

In the [Build a Basic Wallet section](basic-wallet.md), we did the hard work of wiring up a secure client and rock-solid key creation and storage structure with a clear plan for key use and management. Now that we have a method for creating an account — and for storing that account's secrets so they're safe and easy to use — we're ready to start making payments. We'll start with XBN payments since they're a little simpler; in the [next sectiion](custom-assets.md), we'll look at how to support payments for other assets.

There isn’t too much that's new or complicated here: we'll be building on what we already have. Again, most of the work will be in `src/components/wallet/`; however, before we dive into that file let’s clean up our project just a touch and add some helpful polish. Namely a loader component.

## Add Loader Component

Hopefully by now you’re familiar with how to generate new Stencil components.

 \`\`\`bash npm run generate \`\`\`

We'll call the component `stellar-loader`, and deselect both test files leaving only the styling. Once you've done that, open `src/components/loader/` and rename the `.css` file to `.scss`. Then replace the `loader.tsx` contents with this:

 \`\`\`tsx import Combinatorics from "js-combinatorics"; import { Component, h, State, Prop } from "@stencil/core"; import { isEqual as loIsEqual, sample as loSample } from "lodash-es"; @Component\({ tag: "stellar-loader", styleUrl: "loader.scss", shadow: true, }\) export class Loader { @State\(\) chances: any = \[\]; @State\(\) chance: any = null; @Prop\(\) interval: any; componentWillLoad\(\) { return new Promise\(\(resolve\) =&gt; { if \(!this.chances.length\) this.generateChances\(9\); if \(!this.interval\) this.interval = setInterval\(\(\) =&gt; this.getChance\(\), 100\); resolve\(\); }\); } generateChances\(int: number\) { const baseN = Combinatorics.baseN\(\[0, 1\], int\); this.chances = baseN.toArray\(\); this.getChance\(\); } getChance\(\) { const chance = loSample\(this.chances\); if \(loIsEqual\(chance, this.chance\)\) this.getChance\(\); else this.chance = chance; } render\(\) { return \( {this.chance.map\(\(int, i\) =&gt; \( \)\)} \); } } \`\`\`

Don’t forget to install new packages!

 \`\`\`bash npm i -D js-combinatorics \`\`\`

It’s a fancy wackadoodle little component which at the end of the day just produces a little loader for use in our action buttons.

![](https://tyler.link/pM4Z2R+)

## Import Methods

We’re now ready to tackle the `src/components/wallet/wallet.ts` file.

 \`\`\`ts import { Component, State, Prop } from "@stencil/core"; import { Server, ServerApi } from "stellar-sdk"; import componentWillLoad from "./events/componentWillLoad"; import render from "./events/render"; import createAccount from "./methods/createAccount"; import updateAccount from "./methods/updateAccount"; import makePayment from "./methods/makePayment"; import copyAddress from "./methods/copyAddress"; import copySecret from "./methods/copySecret"; import signOut from "./methods/signOut"; import setPrompt from "./methods/setPrompt"; import { Prompter } from "@prompt/prompt"; interface StellarAccount { publicKey: string; keystore: string; state?: ServerApi.AccountRecord; } interface Loading { fund?: boolean; pay?: boolean; update?: boolean; } @Component\({ tag: "stellar-wallet", styleUrl: "wallet.scss", shadow: true, }\) export class Wallet { @State\(\) account: StellarAccount; @State\(\) prompter: Prompter = { show: false }; @State\(\) loading: Loading = {}; @State\(\) error: any = null; @Prop\(\) server: Server; // Component events componentWillLoad\(\) {} render\(\) {} // Stellar methods createAccount = createAccount; updateAccount = updateAccount; makePayment = makePayment; copyAddress = copyAddress; copySecret = copySecret; signOut = signOut; // Misc methods setPrompt = setPrompt; } Wallet.prototype.componentWillLoad = componentWillLoad; Wallet.prototype.render = render; \`\`\`

If you’ve followed other tutorials in this series much of this may be review, but we’ll just walk along this file and see exactly what’s going on.

 \`\`\`ts import { Component, State, Prop } from "@stencil/core"; import { Server, ServerApi } from "stellar-sdk"; import componentWillLoad from "./events/componentWillLoad"; // UPDATE import render from "./events/render"; // UPDATE import createAccount from "./methods/createAccount"; // UPDATE import updateAccount from "./methods/updateAccount"; // NEW import makePayment from "./methods/makePayment"; // NEW import copyAddress from "./methods/copyAddress"; import copySecret from "./methods/copySecret"; import signOut from "./methods/signOut"; import setPrompt from "./methods/setPrompt"; import { Prompter } from "@prompt/prompt"; \`\`\`

Imports galore! Nothing really noteworthy here other than you’ll notice we’re importing `./methods/updateAccount` and `./methods/makePayment` methods which we’ll be creating soon. There are a number of updates in the other methods from previous tutorials, and we’ll walk through all of those in a moment as well.

 \`\`\`ts interface StellarAccount { // UPDATE publicKey: string; keystore: string; state?: ServerApi.AccountRecord; } interface Loading { // NEW fund?: boolean; pay?: boolean; update?: boolean; } \`\`\`

Here we’re setting up two TypeScript classes: one for our account and the other for our loading states.

 \`\`\`ts @Component\({ tag: 'stellar-wallet', styleUrl: 'wallet.scss', shadow: true }\) export class Wallet { @State\(\) account: StellarAccount @State\(\) prompter: Prompter = {show: false} @State\(\) loading: Loading = {} // NEW @State\(\) error: any = null @Prop\(\) server: Server // NEW ... } \`\`\`

Here we set up our `@State`’s, those dynamic properties with values that will change and alter the DOM of the component, and our `@Prop`, which in this case will hold a static reference to our Stellar server instance.

## Update Component Events

Next let’s update our two component events `./events/componentWillLoad.ts` and `./events/render.tsx`:

 \`\`\`ts import { Server } from "stellar-sdk"; import { handleError } from "@services/error"; import { get } from "@services/storage"; export default async function componentWillLoad\(\) { try { let keystore = await get\("keyStore"\); this.error = null; this.server = new Server\("https://horizon-testnet.stellar.org"\); if \(keystore\) { keystore = atob\(keystore\); const { publicKey } = JSON.parse\(atob\(JSON.parse\(keystore\).adata\)\); this.account = { publicKey, keystore, }; this.updateAccount\(\); } } catch \(err\) { this.error = handleError\(err\); } } \`\`\`

In Stencil’s `componentWillLoad` method, we set up default values for the States and Props we initialized earlier. Most notably, we’re setting our server and account. You’ll notice we’re using the public `horizon-testnet` for now — we're just learning, and not ready to send live XBN — but in production you’d want to change this to the public `horizon` endpoint or, if you're running your own Horizon, to one of your own Horizon API endpoints.

For the account we’re simply checking to see if a `keyStore` value has been stored, and if so we’re grabbing the public key and keystore from it and adding those to the account `@State`. The `state` value, which is optional, is not set here as we’ll need to run the method `updateAccount()` to find if the account exists, and if so what the state of that account looks like. We’ll get to that method shortly. For now let’s update our `render.tsx` method:

 \`\`\`tsx import { h } from "@stencil/core"; import { has as loHas } from "lodash-es"; export default function render\(\) { return \[, this.account ? \( \[

{this.account.publicKey}  this.copyAddress\(e\)} &gt; Copy Address  this.copySecret\(e\)} &gt; Copy Secret,  this.makePayment\(e\)} &gt; {this.loading.pay ? : null} Make Payment, \] \) : \(  this.createAccount\(e\)} &gt; {this.loading.fund ? : null} Create Account \), this.error ? \(

```text
{JSON.stringify(this.error, null, 2)}
```

 \) : null, loHas\(this.account, "state"\) ? \(

```text

        {JSON.stringify(this.account.state, null, 2)}
```

 \) : null, this.account ? \[  this.updateAccount\(e\)} &gt; {this.loading.update ? : null} Update Account,  this.signOut\(e\)}&gt; Sign Out, \] : null, \]; } \`\`\`

Yikers amirite!? Don’t worry though: it’s actually quite simple if you’ve spent any time with HTML in JS before. What we're looking at are a few ternary operators toggling the UI between different states based on the account status. Basically just a bunch of buttons wired up to their subsequent actions. Turns out creating those buttons is next on our to-do list!

## Create Buttons

`updateAccount` and `makePayment` are new; `createAccount` will just need a few tweaks. Let’s start with that one.

 \`\`\`ts import sjcl from "@tinyanvil/sjcl"; import axios from "axios"; import { Keypair } from "stellar-sdk"; import { handleError } from "@services/error"; import { set } from "@services/storage"; export default async function createAccount\(e: Event\) { try { e.preventDefault\(\); const pincode\_1 = await this.setPrompt\("Enter a keystore pincode"\); const pincode\_2 = await this.setPrompt\("Enter keystore pincode again"\); if \(!pincode\_1 \|\| !pincode\_2 \|\| pincode\_1 !== pincode\_2\) throw "Invalid pincode"; this.error = null; this.loading = { ...this.loading, fund: true }; const keypair = Keypair.random\(\); await axios\( \`https://friendbot.stellar.org?addr=${keypair.publicKey\(\)}\`, \).finally\(\(\) =&gt; \(this.loading = { ...this.loading, fund: false }\)\); this.account = { publicKey: keypair.publicKey\(\), keystore: sjcl.encrypt\(pincode\_1, keypair.secret\(\), { adata: JSON.stringify\({ publicKey: keypair.publicKey\(\), }\), }\), }; await set\("keyStore", btoa\(this.account.keystore\)\); this.updateAccount\(\); } catch \(err\) { this.error = handleError\(err\); } } \`\`\`

## Fund Account Using Friendbot

The only new thing we’re adding here — other than a loading state and an initial `this.updateAccount()` call at the end — is the call to [friendbot.stellar.org](https://friendbot.stellar.org/), which is a testnet tool that we can use to automatically fund our new testnet account with 10,000 XBN. Nice little shortcut to kickstart our development.

 \`\`\`ts await axios\( \`https://friendbot.stellar.org?addr=${keypair.publicKey\(\)}\`, \).finally\(\(\) =&gt; \(this.loading = { ...this.loading, fund: false }\)\); \`\`\`

In production, you would have to find an actual source for funding the account. Some wallets fund users' accounts for them; some require the user to supply the funds.

So that’s the updated `./methods/createAccount.ts` file.

## Update Account Method

Now let’s create two new files for updating the account and making XBN payments.

 \`\`\`bash touch src/components/wallet/methods/{updateAccount,makePayment}.ts \`\`\`

Let’s start with the simpler one, `./methods/updateAccount.ts`

 \`\`\`ts import { omit as loOmit, map as loMap } from "lodash-es"; import { handleError } from "@services/error"; export default async function updateAccount\(e?: Event\) { try { if \(e\) e.preventDefault\(\); this.error = null; this.loading = { ...this.loading, update: true }; await this.server .accounts\(\) .accountId\(this.account.publicKey\) .call\(\) .then\(\(account\) =&gt; { account.balances = loMap\(account.balances, \(balance\) =&gt; loOmit\(balance, \[ "limit", "buying\_liabilities", "selling\_liabilities", "is\_authorized", "last\_modified\_ledger", balance.asset\_type !== "native" ? "asset\_type" : null, \]\), \); this.account = { ...this.account, state: loOmit\(account, \[ "id", "\_links", "sequence", "subentry\_count", "last\_modified\_ledger", "flags", "thresholds", "account\_id", "signers", "paging\_token", "data\_attr", \]\), }; }\) .finally\(\(\) =&gt; \(this.loading = { ...this.loading, update: false }\)\); } catch \(err\) { this.error = handleError\(err\); } } \`\`\`

All we’re doing here is looking up the state of the Stellar account on the ledger and saving it to the `this.account.state`. You’ll also notice we’re omitting several fields from the account and balances for easier readability. You may choose to save these and selectively display the values you care about, but in our example we’re just displaying the raw JSON, so cleaning things up a little is the right move.

`this.account = {...this.account, state: loOmit(account, ['id', ...])}` may feel odd, but it’s just the Stencil way of updating a state’s object key to trigger a re-render of the DOM. You’ll notice `this.loading` follows the same pattern. We’ll make use of this data further down in the `render` method, but for now just know this is how we would grab ahold of the account to get the latest state.

## Make Payment Method

Next let’s break down the main subject method for this tutorial, `./methods/makePayment.ts`:

 \`\`\`ts import sjcl from "@tinyanvil/sjcl"; import { Keypair, Account, TransactionBuilder, BASE\_FEE, Networks, Operation, Asset, } from "stellar-sdk"; import { has as loHas } from "lodash-es"; import { handleError } from "@services/error"; export default async function makePayment\(e: Event\) { try { e.preventDefault\(\); let instructions = await this.setPrompt\("{Amount} {Destination}"\); instructions = instructions.split\(" "\); const pincode = await this.setPrompt\("Enter your keystore pincode"\); if \(!instructions \|\| !pincode\) return; const keypair = Keypair.fromSecret\( sjcl.decrypt\(pincode, this.account.keystore\), \); this.error = null; this.loading = { ...this.loading, pay: true }; await this.server .accounts\(\) .accountId\(keypair.publicKey\(\)\) .call\(\) .then\(\({ sequence }\) =&gt; { const account = new Account\(keypair.publicKey\(\), sequence\); const transaction = new TransactionBuilder\(account, { fee: BASE\_FEE, networkPassphrase: Networks.TESTNET, }\) .addOperation\( Operation.payment\({ destination: instructions\[1\], asset: Asset.native\(\), amount: instructions\[0\], }\), \) .setTimeout\(0\) .build\(\); transaction.sign\(keypair\); return this.server.submitTransaction\(transaction\).catch\(\(err\) =&gt; { if \( // Paying an account which doesn't exist, create it instead loHas\(err, "response.data.extras.result\_codes.operations"\) && err.response.data.status === 400 && err.response.data.extras.result\_codes.operations.indexOf\( "op\_no\_destination", \) !== -1 \) { const transaction = new TransactionBuilder\(account, { fee: BASE\_FEE, networkPassphrase: Networks.TESTNET, }\) .addOperation\( Operation.createAccount\({ destination: instructions\[1\], startingBalance: instructions\[0\], }\), \) .setTimeout\(0\) .build\(\); transaction.sign\(keypair\); return this.server.submitTransaction\(transaction\); } else throw err; }\); }\) .then\(\(res\) =&gt; console.log\(res\)\) .finally\(\(\) =&gt; { this.loading = { ...this.loading, pay: false }; this.updateAccount\(\); }\); } catch \(err\) { this.error = handleError\(err\); } } \`\`\`

This method is quite massive, so let’s break it down further so it's easier to understand exactly what is going on.

 \`\`\`ts export default async function makePayment\(e: Event\) { try { e.preventDefault\(\) let instructions = await this.setPrompt\('{Amount} {Destination}'\) instructions = instructions.split\(' '\) const pincode = await this.setPrompt\('Enter your keystore pincode'\) if \( !instructions \|\| !pincode \) return \`\`\`

We’re going to need a couple pieces of info from the user: the amount of XBN to send, what address to send it to, and the pincode for unlocking the keystore file. We request those asynchronously and cancel out of the method if they aren’t provided.

 \`\`\`ts const keypair = Keypair.fromSecret\( sjcl.decrypt\(pincode, this.account.keystore\), \); this.error = null; this.loading = { ...this.loading, pay: true }; \`\`\`

Next we unpack the keystore with the pincode, reset any existing errors, and trigger the `pay` loading boolean:

 \`\`\`ts await this.server .accounts\(\) .accountId\(keypair.publicKey\(\)\) .call\(\) .then\(\({sequence}\) =&gt; { const account = new Account\(keypair.publicKey\(\), sequence\) const transaction = new TransactionBuilder\(account, { fee: BASE\_FEE, networkPassphrase: Networks.TESTNET }\) .addOperation\(Operation.payment\({ destination: instructions\[1\], asset: Asset.native\(\), amount: instructions\[0\] }\)\) .setTimeout\(0\) .build\(\) transaction.sign\(keypair\) return this.server.submitTransaction\(transaction\) \`\`\`

From there we call the keypair account to retrieve its current sequence number so we can prepare a transaction with a payment operation. We set the destination and amount using the instructions from the prompt we collected and split earlier. Finally, we build, sign, and submit that transaction to the Stellar Horizon API server.

 \`\`\`ts .catch\(\(err\) =&gt; { if \( // Paying an account which doesn't exist, create it instead loHas\(err, 'response.data.extras.result\_codes.operations'\) && err.response.data.status === 400 && err.response.data.extras.result\_codes.operations.indexOf\('op\_no\_destination'\) !== -1 \) { const transaction = new TransactionBuilder\(account, { fee: BASE\_FEE, networkPassphrase: Networks.TESTNET }\) .addOperation\(Operation.createAccount\({ destination: instructions\[1\], startingBalance: instructions\[0\] }\)\) .setTimeout\(0\) .build\(\) transaction.sign\(keypair\) return this.server.submitTransaction\(transaction\) } else throw err }\) \`\`\`

If the account we want to send XBN is unfunded \(and therefore doesn't yet exist on the ledger\), we'll get back `op_no_destination`. This `catch` handles that issue by trying again with a `createAccount` operation. For any other issues we just pass the error on unmodified.

 \`\`\`ts }\) .then\(\(res\) =&gt; console.log\(res\)\) .finally\(\(\) =&gt; { this.loading = {...this.loading, pay: false} this.updateAccount\(\) }\) } catch \(err\) { this.error = handleError\(err\) } } \`\`\`

Finally, we log any success transaction, kill the loader, and `updateAccount` to reflect the new balance in our account after successfully sending XBN. We also have our `catch` block that passes to the `handleError` service. We will render that in a nice error block in the UI.

There we go! That wasn’t so bad right? Pretty simple, and yet from this tutorial we have the power to hold and observe balances, and to make payments using the power of the Stellar ledger. Amazing!

