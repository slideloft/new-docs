---
title: Setup for Anchored Assets
order: 10
---

# setup-for-anchored-assets

import { CodeExample } from "components/CodeExample";

So how do we make use of SEP-0024 to allow deposits and withdrawals of anchored assets? First let’s boot up our project:

[View trustline boilerplate code on GitHub](https://github.com/stellar/stellar-demo-wallet/tree/trustline)

Next, let's think about our goals. What we’re trying to do is communicate with Anchors to get information about the assets they honor, and about the requirements and steps necessary to initiate a deposit or withdrawal on behalf of a user. When a user deposits with an Anchor — by sending dollars to their bank account via ACH, for example — the Anchor will credit their Stellar account with the equivalent amount of tokens. The user can then hold, transfer, or trade those tokens just like any other Stellar asset. When a user withdraws those tokens — generally by making a payment back to the Anchor's Stellar account — the Anchor redeems them for cash in hand or money in the bank. If you’re still a little lost it will all hopefully become clear as we get coding.

This tutorial will consist of a few minor `./events/` updates and two new `./methods/`. Let’s start with the updates first. We actually need to update the core `wallet.ts` component.

## Update Wallet Component

 \`\`\`ts import { Component, State, Prop } from "@stencil/core"; import { Server, ServerApi } from "stellar-sdk"; import componentWillLoad from "./events/componentWillLoad"; // UPDATE import render from "./events/render"; // UPDATE import createAccount from "./methods/createAccount"; import updateAccount from "./methods/updateAccount"; import depositAsset from "./methods/depositAsset"; // NEW import withdrawAsset from "./methods/withdrawAsset"; // NEW import trustAsset from "./methods/trustAsset"; import makePayment from "./methods/makePayment"; import copyAddress from "./methods/copyAddress"; import copySecret from "./methods/copySecret"; import signOut from "./methods/signOut"; import setPrompt from "./methods/setPrompt"; import { Prompter } from "@prompt/prompt"; interface StellarAccount { publicKey: string; keystore: string; state?: ServerApi.AccountRecord; } interface Loading { fund?: boolean; pay?: boolean; trust?: boolean; update?: boolean; deposit?: boolean; // NEW withdraw?: boolean; // NEW } @Component\({ tag: "stellar-wallet", styleUrl: "wallet.scss", shadow: true, }\) export class Wallet { @State\(\) account: StellarAccount; @State\(\) prompter: Prompter = { show: false }; @State\(\) loading: Loading = {}; @State\(\) error: any = null; @Prop\(\) server: Server; @Prop\(\) homeDomain: String; // NEW @Prop\(\) toml: Object; // NEW // Component events componentWillLoad\(\) {} render\(\) {} // Stellar methods createAccount = createAccount; updateAccount = updateAccount; depositAsset = depositAsset; // NEW withdrawAsset = withdrawAsset; // NEW trustAsset = trustAsset; makePayment = makePayment; copyAddress = copyAddress; copySecret = copySecret; signOut = signOut; // Misc methods setPrompt = setPrompt; } Wallet.prototype.componentWillLoad = componentWillLoad; Wallet.prototype.render = render; \`\`\`

You can see from the `// NEW` and `// UPDATE` comments what we are adding and updating. Nothing worth noting here other than near the bottom two new `@Prop`’s.

 \`\`\`ts @Prop\(\) homeDomain: String // NEW @Prop\(\) toml: Object // NEW \`\`\`

We’ll talk more about home domain’s and stellar.toml files in a moment, but take special note of these as they will play a critical roll in connecting tp the world outside of Stellar.

## Add Deposit and Withdraw Buttons

Next let’s add a couple buttons for deposit and withdraw to the `./events/render.tsx`.

 \`\`\`tsx import { h } from "@stencil/core"; import { has as loHas } from "lodash-es"; export default function render\(\) { return \[, this.account ? \( \[

{this.account.publicKey}  this.copyAddress\(e\)} &gt; Copy Address  this.copySecret\(e\)} &gt; Copy Secret,  this.depositAsset\(e\)} &gt; {this.loading.deposit ? : null} Deposit Asset,  this.withdrawAsset\(e\)} &gt; {this.loading.withdraw ? : null} Withdraw Asset,  this.trustAsset\(e\)} &gt; {this.loading.trust ? : null} Trust Asset,  this.makePayment\(e\)} &gt; {this.loading.pay ? : null} Make Payment, \] \) : \(  this.createAccount\(e\)} &gt; {this.loading.fund ? : null} Create Account \), this.error ? \(

```text
{JSON.stringify(this.error, null, 2)}
```

 \) : null, loHas\(this.account, "state"\) ? \(

```text

        {JSON.stringify(this.account.state, null, 2)}
```

 \) : null, this.account ? \[  this.updateAccount\(e\)} &gt; {this.loading.update ? : null} Update Account,  this.signOut\(e\)}&gt; Sign Out, \] : null, \]; } \`\`\`

This is the same as what we did in the previous tutorial except that we're adding two buttons.

 \`\`\`tsx  this.depositAsset\(e\)}&gt;{this.loading.deposit ? : null} Deposit Asset,  this.withdrawAsset\(e\)}&gt;{this.loading.withdraw ? : null} Withdraw Asset, \`\`\`

“Deposit Asset” and “Withdraw Asset” connect to the `this.depositAsset` and `this.withdrawAsset` methods respectively. We’ll create those methods momentarily.

Before that though let’s make a change to the `./events/componentWillLoad.ts` file.

## Update Components

 \`\`\`ts import { Server, StellarTomlResolver } from "stellar-sdk"; import { handleError } from "@services/error"; import { get } from "@services/storage"; export default async function componentWillLoad\(\) { try { let keystore = await get\("keyStore"\); this.error = null; this.server = new Server\("https://horizon-testnet.stellar.org"\); this.homeDomain = "stellar-anchor-server.herokuapp.com"; this.toml = await StellarTomlResolver.resolve\(this.homeDomain\); if \(keystore\) { keystore = atob\(keystore\); const { publicKey } = JSON.parse\(atob\(JSON.parse\(keystore\).adata\)\); this.account = { publicKey, keystore, }; this.updateAccount\(\); } } catch \(err\) { this.error = handleError\(err\); } } \`\`\`

Here, the only changes we're making are to include of the `StellarTomlResolver` from the `stellar-sdk` package and to set the values for `this.homeDomain` and `this.toml`.

 \`\`\`ts this.homeDomain = "stellar-anchor-server.herokuapp.com"; this.toml = await StellarTomlResolver.resolve\(this.homeDomain\); \`\`\`

## About stellar.toml Files

You know what, let’s just go ahead and cover stellar.toml files. A `stellar.toml` file is a static resource that organizations building on Stellar publish on their home domain at `https://{homeDomain}/.well-known/stellar.toml`. By linking their home domain to a Stellar account using a `set_options` operation, they create a verifiable connection from that account to the information published there. To find out everything you'd ever want to know about stellar.toml files, check out \[SEP-1\], which is the complete stellar.toml specification.

Stellar.toml files contain all sorts of information about an organization, the assets they offer, and the integrations they support. Wallets can look at an account, find the home domain, and crawl a stellar.toml to find out pretty much everything they need to know about an Anchor, and that's exactly what the Stellar SDK `StellarTomlResolver.resolve` method does: it pulls in a stellar.toml and parses it.

Let's look at some concrete examples: here’s [StellarX.com’s stellar.toml file](https://www.stellarx.com/.well-known/stellar.toml).

 \`\`\`toml FEDERATION\_SERVER="https://federation.stellarx.com/federation" ACCOUNTS=\[ "GDM4UWTGHCWSTM7Z46PNF4BLH35GS6IUZYBWNNI4VU5KVIHYSIVQ55Y6" \] \[DOCUMENTATION\] ORG\_NAME="Diamond Ltd." ORG\_DBA="StellarX" ORG\_URL="https://www.stellarx.com" ORG\_LOGO="https://www.stellarx.com/emailAssets/stellarx.png" ORG\_DESCRIPTION="The first full-featured trading app for Stellar's universal marketplace" ORG\_PHYSICAL\_ADDRESS="Hamilton, Bermuda" ORG\_OFFICIAL\_EMAIL="support@stellarx.com" \`\`\`

And here's \[AnchorUSD\]'s[3](https://www.anchorusd.com/.well-known/stellar.toml).

 \`\`\`toml \# ----- AnchorUSD Stellar Anchor ----- NETWORK\_PASSPHRASE="Public Global Stellar Network ; September 2015" ACCOUNTS=\["GDUKMGUGDZQK6YHYA5Z6AY2G4XDSZPSZ3SW5UN3ARVMO6QSRDWP5YLEX", "GASWJWFRYE55KC7MGANZMMRBK5NPXT3HMPDQ6SEXZN6ZPWYXVVYBFRTE"\] TRANSFER\_SERVER="https://api.anchorusd.com/transfer/" WEB\_AUTH\_ENDPOINT="https://api.anchorusd.com/api/webauth" \[DOCUMENTATION\] ORG\_NAME="AnchorCoin LLC" ORG\_DBA="AnchorUSD" ORG\_URL="https://www.anchorusd.com" ORG\_LOGO="https://www.anchorusd.com/assets/images/logo/logo.png" ORG\_DESCRIPTION="AnchorUSD develops a stable cryptocurrency backed one-for-one to the US dollar." ORG\_TWITTER="AnchorUSD" ORG\_OFFICIAL\_EMAIL="support@anchorusd.com" \[\[PRINCIPALS\]\] name="Jim Berkley-Danz" email="j@anchorusd.com" twitter="jimdanz" github="jimdanz" \[\[CURRENCIES\]\] code="USD" issuer="GDUKMGUGDZQK6YHYA5Z6AY2G4XDSZPSZ3SW5UN3ARVMO6QSRDWP5YLEX" display\_decimals=2 anchor\_asset\_type="fiat" anchor\_asset="USD" name="US Dollar" desc="Cryptocurrency backed one-for-one to the US dollar. All dollar deposits are held in an audited, US-domiciled escrow account for the exclusive benefit of AnchorUSD token holders." image="https://www.anchorusd.com/img/usdx.png" \`\`\`

You can see the data provided by these companies that identifies who they are, what they do, and what services they provide. In this tutorial, we’re interested in the `[[CURRENCIES]]` they issue as that’s what we’re trying to get ahold of. We’re also looking for the `TRANSFER_SERVER` keyword, which indicates that an Anchor supports SEP-24, and the `WEB_AUTH_ENDPOINT`, which allows a wallet to set up an authenticated user session. Any time you find these three fields, and you’ve found an Anchor you can interoperate with.

Once we’ve found an Anchor that supports deposit and withdrawal, we can begin the process of connecting with them from our wallet. This tutorial builds on the testnet, so from we’ll be use an SDF testing anchor server located at `stellar-anchor-server.herokuapp.com` You can [view the TOML file for this entity](https://stellar-anchor-server.herokuapp.com/.well-known/stellar.toml) here.

