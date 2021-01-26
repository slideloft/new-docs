---
title: List of Operations
order: 30
---

# list of Operations

This is the canonical list of Bantu operations, which lists every Bantu operation along with parameters, error codes, and links to relevant documentation for key SDKs.

For a description of how operations work in Bantu, see [Operations](../glossary/operations.md).

* [Create Account](list-of-operations.md#create-account)
* [Payment](list-of-operations.md#payment)
* [Path Payment Strict Send](list-of-operations.md#path-payment-strict-send)
* [Path Payment Strict Receive](list-of-operations.md#path-payment-strict-receive)
* [Manage Buy Offer](list-of-operations.md#manage-buy-offer)
* [Manage Sell Offer](list-of-operations.md#manage-sell-offer)
* [Create Passive Sell Offer](list-of-operations.md#create-passive-sell-offer)
* [Set Options](list-of-operations.md#set-options)
* [Change Trust](list-of-operations.md#change-trust)
* [Allow Trust](list-of-operations.md#allow-trust)
* [Account Merge](list-of-operations.md#account-merge)
* [Manage Data](list-of-operations.md#manage-data)
* [Bump Sequence](list-of-operations.md#bump-sequence)
* [Create Claimable Balance](list-of-operations.md#create-claimable-balance)
* [Claim Claimable Balance](list-of-operations.md#claim-claimable-balance)
* [Begin Sponsoring Future Reserves](list-of-operations.md#begin-sponsoring-future-reserves)
* [End Sponsoring Future Reserves](list-of-operations.md#end-sponsoring-future-reserves)
* [Revoke Sponsorship](list-of-operations.md#revoke-sponsorship)

## Create Account

[JavaScript](http://stellar.github.io/js-stellar-sdk/Operation.html#.createAccount) \| [Java](http://stellar.github.io/java-stellar-sdk/org/stellar/sdk/CreateAccountOperation.Builder.html) \| [Go](https://godoc.org/github.com/stellar/go/txnbuild#CreateAccount)

Creates and funds a new account with the specified starting balance.

Threshold: Medium

Result: `CreateAccountResult`

Parameters:

| Parameter | Type | Description |
| :--- | :--- | :--- |
| Destination | account ID | Account address that is created and funded. |
| Starting Balance | integer | Amount of XBN to send to the newly created account. This XBN comes from the source account. |

Possible errors:

| Error | Code | Description |
| :--- | :--- | :--- |
| CREATE\_ACCOUNT\_MALFORMED | -1 | The `destination` is invalid. |
| CREATE\_ACCOUNT\_UNDERFUNDED | -2 | The source account performing the command does not have enough funds to give `destination` the `starting balance` amount of XBN and still maintain its minimum XBN reserve plus satisfy its XBN selling liabilities. |
| CREATE\_ACCOUNT\_LOW\_RESERVE | -3 | This operation would create an account with fewer than the minimum number of XBN an account must hold. |
| CREATE\_ACCOUNT\_ALREADY\_EXIST | -4 | The `destination` account already exists. |

## Payment

[JavaScript](http://stellar.github.io/js-stellar-sdk/Operation.html#.payment) \| [Java](http://stellar.github.io/java-stellar-sdk/org/stellar/sdk/PaymentOperation.Builder.html) \| [Go](https://godoc.org/github.com/stellar/go/txnbuild#Payment)

Sends an amount in a specific asset to a destination account.

Threshold: Medium

Result: `PaymentResult`

Parameters:

| Parameters | Type | Description |
| :--- | :--- | :--- |
| Destination | account ID | Account address that receives the payment. |
| Asset | asset | Asset to send to the destination account. |
| Amount | integer | Amount of the aforementioned asset to send. |

Possible errors:

| Error | Code | Description |
| :--- | :--- | :--- |
| PAYMENT\_MALFORMED | -1 | The input to the payment is invalid. |
| PAYMENT\_UNDERFUNDED | -2 | The source account \(sender\) does not have enough funds to send `amount` and still satisfy its selling liabilities. Note that if seding XBN then the sender must additionally maintain its minimum XBN reserve. |
| PAYMENT\_SRC\_NO\_TRUST | -3 | The source account does not trust the issuer of the asset it is trying to send. |
| PAYMENT\_SRC\_NOT\_AUTHORIZED | -4 | The source account is not authorized to send this payment. |
| PAYMENT\_NO\_DESTINATION | -5 | The receiving account does not exist. |
| PAYMENT\_NO\_TRUST | -6 | The receiver does not trust the issuer of the asset being sent. For more information, see the [assets doc](../glossary/assets.md). |
| PAYMENT\_NOT\_AUTHORIZED | -7 | The destination account is not authorized by the asset's issuer to hold the asset. |
| PAYMENT\_LINE\_FULL | -8 | The destination account \(receiver\) does not have sufficient limits to receive `amount` and still satisfy its buying liabilities. |
| PAYMENT\_NO\_ISSUER | -9 | The issuer of the asset does not exist. |

## Path Payment Strict Send

[JavaScript](http://stellar.github.io/js-stellar-sdk/Operation.html#.pathPaymentStrictSend) \| [Java](http://stellar.github.io/java-stellar-sdk/org/stellar/sdk/PathPaymentStrictSendOperation.Builder.html) \| [Go](https://godoc.org/github.com/stellar/go/txnbuild#PathPaymentStrictSend)

A path payment sends an amount of a specific asset to a destination account through a path of offers. Since the asset sent \(e.g., 450 XBN\) can be different from the asset received \(e.g, 6 BTC\), path payments allow for the simultaneous transfer and conversion of currencies.

A Path Payment Strict Send allows a user to specify the _amount of the asset to send_. The amount received will vary based on offers in the order books. If you would like to instead specify the amount received, use the [Path Payment Strict Receive](list-of-operations.md#path-payment-strict-receive) operation.

A few things to note:

* path payments don't allow intermediate offers to be from the source account as this would yield a worse exchange rate. You'll need to either split the path payment into two smaller path payments, or ensure that the source account's offers are not at the top of the order book.
* balances are settled at the very end of the operation
  * this is especially important when `(Destination, Destination Asset) == (Source, Send Asset)` as this provides a functionality equivalent to getting a no interest loan for the duration of the operation.
* `Destination min` is a protective measure: it allows you to specify a lower bound for an acceptable conversion. If offers in the order books are not favorable enough for the operation to deliver that amount, the operation will fail.

Threshold: Medium

Result: `PathPaymentStrictSendResult`

Parameters:

| Parameters | Type | Description |
| :--- | :--- | :--- |
| Send asset | asset | The asset deducted from the sender's account. |
| Send amount | integer | The amount of `send asset` to deduct \(excluding fees\). |
| Destination | account ID | Account ID of the recipient. |
| Destination asset | asset | The asset the destination account receives. |
| Destination min | integer | The minimum amount of `destination asset` the destination account can receive. |
| Path | list of assets | The assets \(other than `send asset` and `destination asset`\) involved in the offers the path takes. For example, if you can only find a path from USD to EUR through XBN and BTC, the path would be USD -&gt; XBN -&gt; BTC -&gt; EUR and the `path` field would contain XBN and BTC. |

Possible errors:

| Error | Code | Description |
| :--- | :--- | :--- |
| PATH\_PAYMENT\_STRICT\_SEND\_MALFORMED | -1 | The input to this path payment is invalid. |
| PATH\_PAYMENT\_STRICT\_SEND\_UNDERFUNDED | -2 | The source account \(sender\) does not have enough funds to send and still satisfy its selling liabilities. Note that if sending XBN then the sender must additionally maintain its minimum XBN reserve. |
| PATH\_PAYMENT\_STRICT\_SEND\_SRC\_NO\_TRUST | -3 | The source account does not trust the issuer of the asset it is trying to send. |
| PATH\_PAYMENT\_STRICT\_SEND\_SRC\_NOT\_AUTHORIZED | -4 | The source account is not authorized to send this payment. |
| PATH\_PAYMENT\_STRICT\_SEND\_NO\_DESTINATION | -5 | The destination account does not exist. |
| PATH\_PAYMENT\_STRICT\_SEND\_NO\_TRUST | -6 | The destination account does not trust the issuer of the asset being sent. For more, see the [assets doc](../glossary/assets.md). |
| PATH\_PAYMENT\_STRICT\_SEND\_NOT\_AUTHORIZED | -7 | The destination account is not authorized by the asset's issuer to hold the asset. |
| PATH\_PAYMENT\_STRICT\_SEND\_LINE\_FULL | -8 | The destination account does not have sufficient limits to receive `destination amount` and still satisfy its buying liabilities. |
| PATH\_PAYMENT\_STRICT\_SEND\_NO\_ISSUER | -9 | The issuer of one of the assets is missing. |
| PATH\_PAYMENT\_STRICT\_SEND\_TOO\_FEW\_OFFERS | -10 | There is no path of offers connecting the `send asset` and `destination asset`. Stellar only considers paths of length 5 or shorter. |
| PATH\_PAYMENT\_STRICT\_SEND\_OFFER\_CROSS\_SELF | -11 | The payment would cross one of its own offers. |
| PATH\_PAYMENT\_STRICT\_SEND\_UNDER\_DESTMIN | -12 | The paths that could send `destination amount` of `destination asset` would fall short of `destination min`. |

## Path Payment Strict Receive

[JavaScript](https://stellar.github.io/js-stellar-sdk/Operation.html#.pathPaymentStrictReceive) \| [Java](https://stellar.github.io/java-stellar-sdk/org/stellar/sdk/PathPaymentStrictReceiveOperation.Builder.html) \| [Go](https://godoc.org/github.com/stellar/go/txnbuild#PathPaymentStrictReceive)

A path payment sends an amount of a specific asset to a destination account through a path of offers. Since the asset sent \(e.g., 450 XBN\) can be different from the asset received \(e.g, 6 BTC\), path payments allow for the simultaneous transfer and conversion of currencies.

A Path Payment Strict Receive allows a user to specify the _amount of the asset received_. The amount sent varies based on offers in the order books. If you would like to instead specify the amount sent, use the [Path Payment Strict Send](list-of-operations.md#path-payment-strict-send) operation.

A few things to note:

* path payment doesn't allow intermediate offers to be from the source account as this would yield a worse exchange rate. You'll need to either split the path payment into two smaller path payments, or ensure that the source account's offers are not at the top of the order book.
* balances are settled at the very end of the operation
  * this is especially important when `(Destination, Destination Asset) == (Source, Send Asset)` as this provides a functionality equivalent to getting a no interest loan for the duration of the operation.
* `Send max` is a protective measure: it allows you to specify an upper bound for an acceptable conversion. If offers in the order books are not favorable enough for the operation to succeed for less than `Send max`, the operation will fail.

Threshold: Medium

Result: `PathPaymentStrictReceiveResult`

Parameters:

| Parameters | Type | Description |
| :--- | :--- | :--- |
| Send asset | asset | The asset deducted from the sender's account. |
| Send max | integer | The maximum amount of `send asset` to deduct \(excluding fees\). |
| Destination | account ID | Account ID of the recipient. |
| Destination asset | asset | The asset the destination account receives. |
| Destination amount | integer | The amount of `destination asset` the destination account receives. |
| Path | list of assets | The assets \(other than `send asset` and `destination asset`\) involved in the offers the path takes. For example, if you can only find a path from USD to EUR through XBN and BTC, the path would be USD -&gt; XBN -&gt; BTC -&gt; EUR and the `path` field would contain XBN and BTC. |

Possible errors:

| Error | Code | Description |
| :--- | :--- | :--- |
| PATH\_PAYMENT\_STRICT\_RECEIVE\_MALFORMED | -1 | The input to this path payment is invalid. |
| PATH\_PAYMENT\_STRICT\_RECEIVE\_UNDERFUNDED | -2 | The source account \(sender\) does not have enough funds to send and still satisfy its selling liabilities. Note that if sending XBN then the sender must additionally maintain its minimum XBN reserve. |
| PATH\_PAYMENT\_STRICT\_RECEIVE\_SRC\_NO\_TRUST | -3 | The source account does not trust the issuer of the asset it is trying to send. |
| PATH\_PAYMENT\_STRICT\_RECEIVE\_SRC\_NOT\_AUTHORIZED | -4 | The source account is not authorized to send this payment. |
| PATH\_PAYMENT\_STRICT\_RECEIVE\_NO\_DESTINATION | -5 | The destination account does not exist. |
| PATH\_PAYMENT\_STRICT\_RECEIVE\_NO\_TRUST | -6 | The destination account does not trust the issuer of the asset being sent. For more, see the [assets doc](../glossary/assets.md). |
| PATH\_PAYMENT\_STRICT\_RECEIVE\_NOT\_AUTHORIZED | -7 | The destination account is not authorized by the asset's issuer to hold the asset. |
| PATH\_PAYMENT\_STRICT\_RECEIVE\_LINE\_FULL | -8 | The destination account does not have sufficient limits to receive `destination amount` and still satisfy its buying liabilities. |
| PATH\_PAYMENT\_STRICT\_RECEIVE\_NO\_ISSUER | -9 | The issuer of one the of assets is missing. |
| PATH\_PAYMENT\_STRICT\_RECEIVE\_TOO\_FEW\_OFFERS | -10 | There is no path of offers connecting the `send asset` and `destination asset`. Stellar only considers paths of length 5 or shorter. |
| PATH\_PAYMENT\_STRICT\_RECEIVE\_OFFER\_CROSS\_SELF | -11 | The payment would cross one of its own offers. |
| PATH\_PAYMENT\_STRICT\_RECEIVE\_OVER\_SENDMAX | -12 | The paths that could send `destination amount` of `destination asset` would exceed `send max`. |

## Manage Buy Offer

[JavaScript](http://stellar.github.io/js-stellar-sdk/Operation.html#.manageBuyOffer) \| [Java](https://stellar.github.io/java-stellar-sdk/org/stellar/sdk/ManageBuyOfferOperation.Builder.html) \| [Go](https://godoc.org/github.com/stellar/go/txnbuild#ManageBuyOffer)

Creates, updates, or deletes an offer to buy one asset for another, otherwise known as a "bid" order on a traditional orderbook.

If you want to create a new offer set Offer ID to `0`.

If you want to update an existing offer set Offer ID to existing offer ID.

If you want to delete an existing offer set Offer ID to existing offer ID and set Amount to `0`.

Threshold: Medium

Result: `ManageBuyOfferResult`

| Parameters | Type | Description |
| :--- | :--- | :--- |
| Selling | asset | Asset the offer creator is selling. |
| Buying | asset | Asset the offer creator is buying. |
| Amount | integer | Amount of `buying` being bought. Set to `0` if you want to delete an existing offer. |
| Price | {numerator, denominator} | Price of 1 unit of `buying` in terms of `selling`. For example, if you wanted to buy 30 XBN and sell 5 BTC, the price would be {5,30}. |
| Offer ID | unsigned integer | The ID of the offer. `0` for new offer. Set to existing offer ID to update or delete. |

Possible errors:

| Error | Code | Description |
| :--- | :--- | :--- |
| MANAGE\_BUY\_OFFER\_MALFORMED | -1 | The input is incorrect and would result in an invalid offer. |
| MANAGE\_BUY\_OFFER\_SELL\_NO\_TRUST | -2 | The account creating the offer does not have a trustline for the asset it is selling. |
| MANAGE\_BUY\_OFFER\_BUY\_NO\_TRUST | -3 | The account creating the offer does not have a trustline for the asset it is buying. |
| MANAGE\_BUY\_OFFER\_BUY\_NOT\_AUTHORIZED | -4 | The account creating the offer is not authorized to sell this asset. |
| MANAGE\_BUY\_OFFER\_SELL\_NOT\_AUTHORIZED | -5 | The account creating the offer is not authorized to buy this asset. |
| MANAGE\_BUY\_OFFER\_LINE\_FULL | -6 | The account creating the offer does not have sufficient limits to receive `buying` and still satisfy its buying liabilities. |
| MANAGE\_BUY\_OFFER\_UNDERFUNDED | -7 | The account creating the offer does not have sufficient limits to send `selling` and still satisfy its selling liabilities. Note that if selling XBN then the account must additionally maintain its minimum XBN reserve, which is calculated assuming this offer will not completely execute immediately. |
| MANAGE\_BUY\_OFFER\_CROSS\_SELF | -8 | The account has opposite offer of equal or lesser price active, so the account creating this offer would immediately cross itself. |
| MANAGE\_BUY\_OFFER\_SELL\_NO\_ISSUER | -9 | The issuer of selling asset does not exist. |
| MANAGE\_BUY\_OFFER\_BUY\_NO\_ISSUER | -10 | The issuer of buying asset does not exist. |
| MANAGE\_BUY\_OFFER\_NOT\_FOUND | -11 | An offer with that `offerID` cannot be found. |
| MANAGE\_BUY\_OFFER\_LOW\_RESERVE | -12 | The account creating this offer does not have enough XBN to satisfy the minimum XBN reserve increase caused by adding a subentry and still satisfy its XBN selling liabilities. For every offer an account creates, the minimum amount of XBN that account must hold will increase. |

## Manage Sell Offer

[JavaScript](http://stellar.github.io/js-stellar-sdk/Operation.html#.manageSellOffer) \| [Java](https://stellar.github.io/java-stellar-sdk/org/stellar/sdk/ManageSellOfferOperation.Builder.html) \| [Go](https://godoc.org/github.com/stellar/go/txnbuild#ManageSellOffer)

Creates, updates, or deletes an offer to sell one asset for another, otherwise known as a "ask" order or "offer" on a traditional orderbook.

If you want to create a new offer set Offer ID to `0`.

If you want to update an existing offer set Offer ID to existing offer ID.

If you want to delete an existing offer set Offer ID to existing offer ID and set Amount to `0`.

Threshold: Medium

Result: `ManageSellOfferResult`

| Parameters | Type | Description |
| :--- | :--- | :--- |
| Selling | asset | Asset the offer creator is selling. |
| Buying | asset | Asset the offer creator is buying. |
| Amount | integer | Amount of `selling` being sold. Set to `0` if you want to delete an existing offer. |
| Price | {numerator, denominator} | Price of 1 unit of `selling` in terms of `buying`. For example, if you wanted to sell 30 XBN and buy 5 BTC, the price would be {5,30}. |
| Offer ID | unsigned integer | The ID of the offer. `0` for new offer. Set to existing offer ID to update or delete. |

Possible errors:

| Error | Code | Description |
| :--- | :--- | :--- |
| MANAGE\_SELL\_OFFER\_MALFORMED | -1 | The input is incorrect and would result in an invalid offer. |
| MANAGE\_SELL\_OFFER\_SELL\_NO\_TRUST | -2 | The account creating the offer does not have a trustline for the asset it is selling. |
| MANAGE\_SELL\_OFFER\_BUY\_NO\_TRUST | -3 | The account creating the offer does not have a trustline for the asset it is buying. |
| MANAGE\_SELL\_OFFER\_SELL\_NOT\_AUTHORIZED | -4 | The account creating the offer is not authorized to sell this asset. |
| MANAGE\_SELL\_OFFER\_BUY\_NOT\_AUTHORIZED | -5 | The account creating the offer is not authorized to buy this asset. |
| MANAGE\_SELL\_OFFER\_LINE\_FULL | -6 | The account creating the offer does not have sufficient limits to receive `buying` and still satisfy its buying liabilities. |
| MANAGE\_SELL\_OFFER\_UNDERFUNDED | -7 | The account creating the offer does not have sufficient limits to send `selling` and still satisfy its selling liabilities. Note that if selling XBN then the account must additionally maintain its minimum XBN reserve, which is calculated assuming this offer will not completely execute immediately. |
| MANAGE\_SELL\_OFFER\_CROSS\_SELF | -8 | The account has opposite offer of equal or lesser price active, so the account creating this offer would immediately cross itself. |
| MANAGE\_SELL\_OFFER\_SELL\_NO\_ISSUER | -9 | The issuer of selling asset does not exist. |
| MANAGE\_SELL\_OFFER\_BUY\_NO\_ISSUER | -10 | The issuer of buying asset does not exist. |
| MANAGE\_SELL\_OFFER\_NOT\_FOUND | -11 | An offer with that `offerID` cannot be found. |
| MANAGE\_SELL\_OFFER\_LOW\_RESERVE | -12 | The account creating this offer does not have enough XBN to satisfy the minimum XBN reserve increase caused by adding a subentry and still satisfy its XBN selling liabilities. For every offer an account creates, the minimum amount of XBN that account must hold will increase. |

## Create Passive Sell Offer

[JavaScript](https://stellar.github.io/js-stellar-sdk/Operation.html#.createPassiveSellOffer) \| [Java](https://stellar.github.io/java-stellar-sdk/org/stellar/sdk/CreatePassiveSellOfferOperation.Builder.html) \| [Go](https://godoc.org/github.com/stellar/go/txnbuild#CreatePassiveSellOffer)

Creates, updates, or deletes an offer to sell one asset for another, otherwise known as a "ask" order or "offer" on a traditional orderbook, _without taking a reverse offer of equal price_.

A passive sell offer is an offer that does not act on and take a reverse offer of equal price. Instead, they only take offers of lesser price. For example, if an offer exists to buy 5 BTC for 30 XBN, and you make a passive offer to buy 30 XBN for 5 BTC, your passive offer _does not_ take the first offer. Passive offers in Stellar are always expressed as "ask" or "offer" orders in a traditional orderbook.

Note that regular offers made later than your passive offer can act on and take your passive offer, even if the regular offer is of the same price as your passive offer.

Passive offers allow market makers to have zero spread. If you want to trade EUR for USD at 1:1 price and USD for EUR also at 1:1, you can create two passive offers so the two offers don't immediately act on each other.

Once the passive offer is created, you can manage it like any other offer using the [manage sell offer](list-of-operations.md#manage-sell-offer) operation.

Threshold: Medium

Result: `ManageSellOfferResult`

| Parameters | Type | Description |
| :--- | :--- | :--- |
| Selling | asset | Asset the offer creator is selling. |
| Buying | asset | Asset the offer creator is buying. |
| Amount | integer | Amount of `selling` being sold. Set to `0` if you want to delete an existing offer. |
| Price | {numerator, denominator} | Price of 1 unit of `selling` in terms of `buying`. For example, if you wanted to sell 30 XBN and buy 5 BTC, the price would be {5,30}. |

Possible errors:

| Error | Code | Description |
| :--- | :--- | :--- |
| MANAGE\_SELL\_OFFER\_MALFORMED | -1 | The input is incorrect and would result in an invalid offer. |
| MANAGE\_SELL\_OFFER\_SELL\_NO\_TRUST | -2 | The account creating the offer does not have a trustline for the asset it is selling. |
| MANAGE\_SELL\_OFFER\_BUY\_NO\_TRUST | -3 | The account creating the offer does not have a trustline for the asset it is buying. |
| MANAGE\_SELL\_OFFER\_SELL\_NOT\_AUTHORIZED | -4 | The account creating the offer is not authorized to sell this asset. |
| MANAGE\_SELL\_OFFER\_BUY\_NOT\_AUTHORIZED | -5 | The account creating the offer is not authorized to buy this asset. |
| MANAGE\_SELL\_OFFER\_LINE\_FULL | -6 | The account creating the offer does not have sufficient limits to receive `buying` and still satisfy its buying liabilities. |
| MANAGE\_SELL\_OFFER\_UNDERFUNDED | -7 | The account creating the offer does not have sufficient limits to send `selling` and still satisfy its selling liabilities. Note that if selling XBN then the account must additionally maintain its minimum XBN reserve, which is calculated assuming this offer will not completely execute immediately. |
| MANAGE\_SELL\_OFFER\_CROSS\_SELF | -8 | The account has opposite offer of equal or lesser price active, so the account creating this offer would immediately cross itself. |
| MANAGE\_SELL\_OFFER\_SELL\_NO\_ISSUER | -9 | The issuer of selling asset does not exist. |
| MANAGE\_SELL\_OFFER\_BUY\_NO\_ISSUER | -10 | The issuer of buying asset does not exist. |
| MANAGE\_SELL\_OFFER\_NOT\_FOUND | -11 | An offer with that `offerID` cannot be found. |
| MANAGE\_SELL\_OFFER\_LOW\_RESERVE | -12 | The account creating this offer does not have enough XBN to satisfy the minimum XBN reserve increase caused by adding a subentry and still satisfy its XBN selling liabilities. For every offer an account creates, the minimum amount of XBN that account must hold will increase. |

## Set Options

[JavaScript](http://stellar.github.io/js-stellar-sdk/Operation.html#.setOptions) \| [Java](http://stellar.github.io/java-stellar-sdk/org/stellar/sdk/SetOptionsOperation.Builder.html) \| [Go](https://godoc.org/github.com/stellar/go/txnbuild#SetOptions)

Sets options for an account, such as setting the inflation destination or adding an additional signer on an account.

Allows you to set multiple options on an account in a single operation, such as changing an operation threshold and setting the flags on an account at the same time.

For more information on the options related to signing, see our docs on [multi-sig](../glossary/multisig.md).

When updating signers or other thresholds, the threshold of this operation is High.

Threshold: Medium or High

Result: `SetOptionsResult`

Parameters:

| Parameters | Type | Description |
| :--- | :--- | :--- |
| Inflation Destination | account ID | Account of the inflation destination. |
| Clear flags | integer | Indicates which flags to clear. For details about the flags, please refer to the [accounts doc](../glossary/accounts.md). The bit mask integer subtracts from the existing flags of the account. This allows for setting specific bits without knowledge of existing flags. |
| Set flags | integer | Indicates which flags to set. For details about the flags, please refer to the [accounts doc](../glossary/accounts.md). The bit mask integer adds onto the existing flags of the account. This allows for setting specific bits without knowledge of existing flags. |
| Master weight | integer | A number from 0-255 \(inclusive\) representing the weight of the master key. If the weight of the master key is updated to 0, it is effectively disabled. |
| Low threshold | integer | A number from 0-255 \(inclusive\) representing the threshold this account sets on all operations it performs that have [a low threshold](../glossary/multisig.md). |
| Medium threshold | integer | A number from 0-255 \(inclusive\) representing the threshold this account sets on all operations it performs that have [a medium threshold](../glossary/multisig.md). |
| High threshold | integer | A number from 0-255 \(inclusive\) representing the threshold this account sets on all operations it performs that have [a high threshold](../glossary/multisig.md). |
| Home domain | string | Sets the home domain of an account. See [Federation](../glossary/federation.md). |
| Signer | {Public Key, weight} | Add, update, or remove a signer from an account. Signer weight is a number from 0-255 \(inclusive\). The signer is deleted if the weight is 0. |

Possible errors:

| Error | Code | Description |
| :--- | :--- | :--- |
| SET\_OPTIONS\_LOW\_RESERVE | -1 | This account does not have enough XBN to satisfy the minimum XBN reserve increase caused by adding a subentry and still satisfy its XBN selling liabilities. For every new signer added to an account, the minimum reserve of XBN that account must hold increases. |
| SET\_OPTIONS\_TOO\_MANY\_SIGNERS | -2 | 20 is the maximum number of signers an account can have, and adding another signer would exceed that. |
| SET\_OPTIONS\_BAD\_FLAGS | -3 | The flags set and/or cleared are invalid by themselves or in combination. |
| SET\_OPTIONS\_INVALID\_INFLATION | -4 | The destination account set in the `inflation` field does not exist. |
| SET\_OPTIONS\_CANT\_CHANGE | -5 | This account can no longer change the option it wants to change. |
| SET\_OPTIONS\_UNKNOWN\_FLAG | -6 | The account is trying to set a flag that is unknown. |
| SET\_OPTIONS\_THRESHOLD\_OUT\_OF\_RANGE | -7 | The value for a key weight or threshold is invalid. |
| SET\_OPTIONS\_BAD\_SIGNER | -8 | Any additional signers added to the account cannot be the master key. |
| SET\_OPTIONS\_INVALID\_HOME\_DOMAIN | -9 | Home domain is malformed. |

## Change Trust

[JavaScript](http://stellar.github.io/js-stellar-sdk/Operation.html#.changeTrust) \| [Java](http://stellar.github.io/java-stellar-sdk/org/stellar/sdk/ChangeTrustOperation.Builder.html) \| [Go](https://godoc.org/github.com/stellar/go/txnbuild#ChangeTrust)

Creates, updates, or deletes a trustline. For more on trustlines, please refer to the [assets documentation](../glossary/assets.md).

To delete an existing trustline, set Line to the asset of the trustline, and Limit to `0`.

Threshold: Medium

Result: `ChangeTrustResult`

| Parameters | Type | Description |
| :--- | :--- | :--- |
| Line | asset | The asset of the trustline. For example, if a user extends a trustline of up to 200 USD to an anchor, the `line` is USD:anchor. |
| Limit | integer | The limit of the trustline. In the previous example, the `limit` would be 200. |

Possible errors:

| Error | Code | Description |
| :--- | :--- | :--- |
| CHANGE\_TRUST\_MALFORMED | -1 | The input to this operation is invalid. |
| CHANGE\_TRUST\_NO\_ISSUER | -2 | The issuer of the asset cannot be found. |
| CHANGE\_TRUST\_INVALID\_LIMIT | -3 | The `limit` is not sufficient to hold the current balance of the trustline and still satisfy its buying liabilities. |
| CHANGE\_TRUST\_LOW\_RESERVE | -4 | This account does not have enough XBN to satisfy the minimum XBN reserve increase caused by adding a subentry and still satisfy its XBN selling liabilities. For every new trustline added to an account, the minimum reserve of XBN that account must hold increases. |
| CHANGE\_TRUST\_SELF\_NOT\_ALLOWED | -5 | The source account attempted to create a trustline for itself, which is not allowed. |

## Allow Trust

[JavaScript](http://stellar.github.io/js-stellar-sdk/Operation.html#.allowTrust) \| [Java](http://stellar.github.io/java-stellar-sdk/org/stellar/sdk/AllowTrustOperation.Builder.html) \| [Go](https://godoc.org/github.com/stellar/go/txnbuild#AllowTrust)

Updates the `authorized` flag of an existing trustline.

This can only be called by the issuer of a trustline's [asset](../glossary/assets.md), and only when `AUTHORIZATION REQUIRED` has been set on the issuer's account.

There are two different kinds of asset authorization: complete authorization, which allows an account to transact with an asset \(by making payments, creating offers, etc.\) and limited authorization, which allows an account to maintain and reduce current offers, but not to perform other operations with the asset.

The issuer can only change a flag from complete to limited authorization or clear the `authorized` flag if the issuer has the `AUTH_REVOCABLE_FLAG` set. Otherwise, the issuer can only set the `authorized` flag. For more on what toggling between authorization states allows an issuer to do, see the [Control Access to an Asset](../issuing-assets/control-asset-access.md) doc.

If the issuer clears the `authorized` flag, all offers owned by the `trustor` that are either selling `type` or buying `type` will be deleted.

Threshold: Low

Result: `AllowTrustResult`

| Parameters | Type | Description |
| :--- | :--- | :--- |
| Trustor | account ID | The account of the recipient of the trustline. |
| Type | asset code | The 4 or 12 character-maximum asset code of the trustline the source account is authorizing. For example, if an issuing account wants to allow another account to hold its USD credit, the `type` is `USD`. |
| Authorize | integer | Flag indicating whether the trustline is authorized. `1` if the account is authorized to transact with the asset. `2` if the account is authorized to maintain offers, but not to perform other transactions |

Possible errors:

| Error | Code | Description |
| :--- | :--- | :--- |
| ALLOW\_TRUST\_MALFORMED | -1 | The asset specified in `type` is invalid. In addition, this error happens when the native asset is specified. |
| ALLOW\_TRUST\_NO\_TRUST\_LINE | -2 | The `trustor` does not have a trustline with the issuer performing this operation. |
| ALLOW\_TRUST\_TRUST\_NOT\_REQUIRED | -3 | The source account \(issuer performing this operation\) does not require trust. In other words, it does not have the flag `AUTH_REQUIRED_FLAG` set. |
| ALLOW\_TRUST\_CANT\_REVOKE | -4 | The source account is trying to revoke the trustline of the `trustor`, but it cannot do so. |
| ALLOW\_TRUST\_SELF\_NOT\_ALLOWED | -5 | The source account attempted to allow a trustline for itself, which is not allowed because an account cannot create a trustline with itself. |

## Account Merge

[JavaScript](http://stellar.github.io/js-stellar-sdk/Operation.html#.accountMerge) \| [Java](http://stellar.github.io/java-stellar-sdk/org/stellar/sdk/AccountMergeOperation.Builder.html) \| [Go](https://godoc.org/github.com/stellar/go/txnbuild#AccountMerge)

Transfers the native balance \(the amount of XBN an account holds\) to another account and removes the source account from the ledger.

Threshold: High

Result: `AccountMergeResult`

| Parameters | Type | Description |
| :--- | :--- | :--- |
| Destination | account ID | The account that receives the remaining XBN balance of the source account. |

Possible errors:

| Error | Code | Description |
| :--- | :--- | :--- |
| ACCOUNT\_MERGE\_MALFORMED | -1 | The operation is malformed because the source account cannot merge with itself. The `destination` must be a different account. |
| ACCOUNT\_MERGE\_NO\_ACCOUNT | -2 | The `destination` account does not exist. |
| ACCOUNT\_MERGE\_IMMUTABLE\_SET | -3 | The source account has `AUTH_IMMUTABLE` flag set. |
| ACCOUNT\_MERGE\_HAS\_SUB\_ENTRIES | -4 | The source account has trust lines/offers. |
| ACCOUNT\_MERGE\_SEQNUM\_TOO\_FAR | -5 | Source's account sequence number is too high. It must be less than `(ledgerSeq << 32) = (ledgerSeq * 0x100000000)`. |
| ACCOUNT\_MERGE\_DEST\_FULL | -6 | The `destination` account cannot receive the balance of the source account and still satisfy its lumen buying liabilities. |
| ACCOUNT\_MERGE\_IS\_SPONSOR | -7 | The source account is a sponsor. |

## Manage Data

[JavaScript](http://stellar.github.io/js-stellar-sdk/Operation.html#.manageData) \| [Java](http://stellar.github.io/java-stellar-sdk/org/stellar/sdk/ManageDataOperation.Builder.html) \| [Go](https://godoc.org/github.com/stellar/go/txnbuild#ManageData)

Sets, modifies, or deletes a data entry \(name/value pair\) that is attached to a particular account.

An account can have a large amount of data entries attached to it \(subject to sub-entry limits for an account\). Each data entry increases the minimum balance \(via the base reserve\) needed to be held by the account.

Data entries can be used for storing application-specific data on the Stellar Network. They are not used by the core Stellar Protocol.

Threshold: Medium

Result: `ManageDataResult`

| Parameters | Type | Description |
| :--- | :--- | :--- |
| Name | string | String up to 64 bytes long. If this is a new Name it will add the given name/value pair to the account. If this Name is already present then the associated value will be modified. |
| Value | binary data | \(optional\) If not present then the existing Name will be deleted. If present then this value will be set in the DataEntry. Up to 64 bytes long. |

Possible errors:

| Error | Code | Description |
| :--- | :--- | :--- |
| MANAGE\_DATA\_NOT\_SUPPORTED\_YET | -1 | The network hasn't moved to this protocol change yet. This failure means the network doesn't support this feature yet. |
| MANAGE\_DATA\_NAME\_NOT\_FOUND | -2 | Trying to remove a Data Entry that isn't there. This will happen if Name is set \(and Value isn't\) but the Account doesn't have a DataEntry with that Name. |
| MANAGE\_DATA\_LOW\_RESERVE | -3 | This account does not have enough XBN to satisfy the minimum XBN reserve increase caused by adding a subentry and still satisfy its XBN selling liabilities. For every new DataEntry added to an account, the minimum reserve of XBN that account must hold increases. |
| MANAGE\_DATA\_INVALID\_NAME | -4 | Name not a valid string. |

## Bump Sequence

[JavaScript](http://stellar.github.io/js-stellar-sdk/Operation.html#.bumpSequence) \| [Java](http://stellar.github.io/java-stellar-sdk/org/stellar/sdk/BumpSequenceOperation.Builder.html) \| [Go](https://godoc.org/github.com/stellar/go/txnbuild#BumpSequence)

Bumps forward the sequence number of the source account to the given sequence number.

This operation invalidates any transactions with a smaller sequence number, and is often utilized in complex contracting scenarios.

If the specified `bumpTo` sequence number is greater than the source account's sequence number, the account's sequence number is updated with that value, otherwise it's not modified.

Threshold: Low

Result: `BumpSequenceResult`

| Parameters | Type | Description |
| :--- | :--- | :--- |
| bumpTo | SequenceNumber | desired value for the operation's source account sequence number. |

Possible errors:

| Error | Code | Description |
| :--- | :--- | :--- |
| BUMP\_SEQUENCE\_BAD\_SEQ | -1 | The specified `bumpTo` sequence number is not a valid sequence number. It must be between 0 and `INT64_MAX` \(9223372036854775807 or 0x7fffffffffffffff\). |

## Create Claimable Balance

Creates a ClaimableBalanceEntry. See [Claimable Balance](../glossary/claimable-balance.md) for more information on parameters and usage.

Threshold: Medium

Result: `CreateClaimableBalanceResult`

| Parameters | Type | Description |
| :--- | :--- | :--- |
| Asset | asset | Asset that will be held in the ClaimableBalanceEntry in the form `asset_code:issuing_address` or `native` \(XBN\). |
| Amount | integer | Amount of `asset` stored in the ClaimableBalanceEntry. |
| Claimants | list of claimants | List of Claimants \(account address and ClaimPredicate pair\) that can claim this ClaimableBalanceEntry. |

Possible errors:

| Error | Code | Description |
| :--- | :--- | :--- |
| CREATE\_CLAIMABLE\_BALANCE\_MALFORMED | -1 | The input to this operation is invalid. |
| CREATE\_CLAIMABLE\_BALANCE\_LOW\_RESERVE | -2 | The account creating this entry does not have enough XBN to satisfy the minimum XBN reserve increase caused by adding a ClaimableBalanceEntry. For every claimant in the list, the minimum amount of XBN this account must hold will increase by baseReserve. |
| CREATE\_CLAIMABLE\_BALANCE\_NO\_TRUST | -3 | The source account does not trust the issuer of the asset it is trying to include in the ClaimableBalanceEntry. |
| CREATE\_CLAIMABLE\_BALANCE\_NOT\_AUTHORIZED | -4 | The source account is not authorized to transfer this asset. |
| CREATE\_CLAIMABLE\_BALANCE\_UNDERFUNDED | -5 | The source account does not have enough funds to transfer `amount` of this asset to the ClaimableBalanceEntry. |

## Claim Claimable Balance

Claims a ClaimableBalanceEntry and adds the amount of asset on the entry to the source account.

Threshold: Low

Result: `ClaimClaimableBalanceResult`

| Parameters | Type | Description |
| :--- | :--- | :--- |
| BalanceID | claimableBalanceID | BalanceID on the ClaimableBalanceEntry that the source account is claiming. The balanceID can be retrieved from a succesful `CreateClaimableBalanceResult`. See [ClaimableBalanceID](../glossary/miscellaneous-core-objects.md#ClaimableBalanceID) for more information. |

Possible errors:

| Error | Code | Description |
| :--- | :--- | :--- |
| CLAIM\_CLAIMABLE\_BALANCE\_DOES\_NOT\_EXIST | -1 | There is no existing ClaimableBalanceEntry that matches the input BalanceID. |
| CLAIM\_CLAIMABLE\_BALANCE\_CANNOT\_CLAIM | -2 | There is no claimant that matches the source account, or the claimants predicate is not satisfied. |
| CLAIM\_CLAIMABLE\_BALANCE\_LINE\_FULL | -3 | The account claiming the ClaimableBalanceEntry does not have sufficient limits to receive amount of the asset and still satisfy its buying liabilities. |
| CLAIM\_CLAIMABLE\_BALANCE\_NO\_TRUST | -4 | The source account does not trust the issuer of the asset it is trying to claim in the ClaimableBalanceEntry. |
| CLAIM\_CLAIMABLE\_BALANCE\_NOT\_AUTHORIZED | -5 | The source account is not authorized to claim the asset in the ClaimableBalanceEntry. |

## Begin Sponsoring Future Reserves

Establishes the is-sponsoring-future-reserves-for relationship between the source account and sponsoredID. See [Sponsored Reserves](../glossary/sponsored-reserves.md) for more information.

There must be a corresponding [end sponsoring future reserves](list-of-operations.md#end-sponsoring-future-reserves) operation in the same transaction to end the is-sponsoring-future-reserves-for relationship. The transaction will fail with `txBAD_SPONSORSHIP` otherwise.

Threshold: Medium

Result: `BeginSponsoringFutureReservesResult`

| Parameters | Type | Description |
| :--- | :--- | :--- |
| SponsoredID | account ID | Account that will have it's reserves sponsored. |

Possible errors:

| Error | Code | Description |
| :--- | :--- | :--- |
| BEGIN\_SPONSORING\_FUTURE\_RESERVES\_MALFORMED | -1 | Source account is equal to sponsoredID. |
| BEGIN\_SPONSORING\_FUTURE\_RESERVES\_ALREADY\_SPONSORED | -2 | Source account is already sponsoring sponsoredID. |
| BEGIN\_SPONSORING\_FUTURE\_RESERVES\_RECURSIVE | -3 | Either source account is currently being sponsored, or sponsoredID is sponsoring another account. |

## End Sponsoring Future Reserves

Terminates the current is-sponsoring-future-reserves-for relationship in which the source account is sponsored.

Threshold: Medium

Result: `EndSponsoringFutureReservesResult`

| Error | Code | Description |
| :--- | :--- | :--- |
| END\_SPONSORING\_FUTURE\_RESERVES\_NOT\_SPONSORED | -1 | Source account is not sponsored. |

## Revoke Sponsorship

The logic of this operation depends on the state of the source account.

If the source account is not sponsored or is sponsored by the owner of the specified entry or sub-entry, then attempt to revoke the sponsorship. If the source account is sponsored, the next step depends on whether the entry is sponsored or not. If it is sponsored, attempt to transfer the sponsorship to the sponsor of the source account. If the entry is not sponsored, then establish the sponsorship.

Threshold: Medium

Result: `RevokeSponsorshipResult`

This operation is a union with **two** possible types -

| Union Type | Parameters | Type | Description |
| :--- | :--- | :--- | :--- |
| REVOKE\_SPONSORSHIP\_LEDGER\_ENTRY | LedgerKey | ledgerKey | Ledger key that holds information to identify a specific ledgerEntry that may have it's sponsorship modified. See [LedgerKey](../glossary/miscellaneous-core-objects.md#LedgerKey) for more information. |

Or

| Union Type | Parameters | Type | Description |
| :--- | :--- | :--- | :--- |
| REVOKE\_SPONSORSHIP\_SIGNER | Signer | {account ID, Signer Key} | Signer that may have it's sponsorship modified. |

Possible errors:

| Error | Code | Description |
| :--- | :--- | :--- |
| REVOKE\_SPONSORSHIP\_DOES\_NOT\_EXIST | -1 | The ledgerEntry for LedgerKey doesn't exist, the account ID on signer doesn't exist, or the Signer Key doesn't exist on account ID's account. |
| REVOKE\_SPONSORSHIP\_NOT\_SPONSOR | -2 | If the ledgerEntry/signer is sponsored, then the source account must be the sponsor. If the ledgerEntry/signer is not sponsored, the source account must be the owner. This error will be thrown otherwise. |
| REVOKE\_SPONSORSHIP\_LOW\_RESERVE | -3 | The sponsored account does not have enough XBN to satisfy the minimum balance increase caused by revoking sponsorship on a ledgerEntry/signer it owns, or the sponsor of the source account doesn't have enough XBN to satisfy the minimum balance increase caused by sponsoring a transfered ledgerEntry/signer. |
| REVOKE\_SPONSORSHIP\_ONLY\_TRANSFERABLE | -4 | Sponsorship cannot be removed from this ledgerEntry. This error will happen if the user tries to remove the sponsorship from a ClaimableBalanceEntry. |

