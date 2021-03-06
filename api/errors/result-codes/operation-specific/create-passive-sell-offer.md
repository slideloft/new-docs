---
title: Create Passive Sell Offer Result Codes
order: 70
---

# Create Passive Sell Offer

These are result codes that communicate success \(200\) or failure \(400\) specific to the `Create Passive Sell Offer` operation.

Learn more about the [`Create Passive Sell Offer` operation](../../../../start/list-of-operations.md#create-passive-sell-offer).

 

* OpSuccess `CREATE_PASSIVE_SELL_OFFER_SUCCESS`

  The passive sell offer was successfully placed.

* OpMalformed `MANAGE_SELL_OFFER_MALFORMED`

  The input is incorrect and would result in an invalid offer.

* op\_sell\_no\_trust `MANAGE_SELL_OFFER_SELL_NO_TRUST`

  The account creating the offer does not have a trustline for the asset it is selling.

* op\_buy\_no\_trust `MANAGE_SELL_OFFER_BUY_NO_TRUST`

  The account creating the offer does not have a trustline for the asset it is buying.

* sell\_not\_authorized `MANAGE_SELL_OFFER_SELL_NOT_AUTHORIZED`

  The account creating the offer is not authorized to sell this asset.

* buy\_not\_authorized `MANAGE_SELL_OFFER_BUY_NOT_AUTHORIZED`

  The account creating the offer is not authorized to buy this asset.

* OpLineFull `MANAGE_SELL_OFFER_LINE_FULL`

  The account creating the offer does not have sufficient limits to receive buying and still satisfy its buying liabilities.

* OpUnderfunded `MANAGE_SELL_OFFER_UNDERFUNDED`

  The account creating the offer does not have sufficient limits to send selling and still satisfy its selling liabilities. Note that if selling XBN then the account must additionally maintain its minimum XBN reserve, which is calculated assuming this offer will not completely execute immediately.

* op\_cross\_self `MANAGE_SELL_OFFER_CROSS_SELF`

  The account has opposite offer of equal or lesser price active, so the account creating this offer would immediately cross itself.

* op\_sell\_no\_issuer `MANAGE_SELL_OFFER_SELL_NO_ISSUER`

  The issuer of selling asset does not exist.

* buy\_no\_issuer `MANAGE_SELL_OFFER_BUY_NO_ISSUER`

  The issuer of buying asset does not exist.

* op\_offer\_not\_found `MANAGE_SELL_OFFER_NOT_FOUND`

  An offer with that offerID cannot be found.

* OpLowReserve `MANAGE_SELL_OFFER_LOW_RESERVE`

  The account creating this offer does not have enough XBN to satisfy the minimum XBN reserve increase caused by adding a subentry and still satisfy its XBN selling liabilities. For every offer an account creates, the minimum amount of XBN that account must hold will increase.

