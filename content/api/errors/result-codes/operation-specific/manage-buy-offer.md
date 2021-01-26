---
title: Manage Buy Offer Result Codes
order: 60
---

# manage-buy-offer

import { ExampleResponse } from "components/ExampleResponse"; import { AttributeTable } from "components/AttributeTable";

These are result codes that communicate success \(200\) or failure \(400\) specific to the `Manage Buy Offer` operation.

Learn more about the [`Manage Buy Offer` operation](../../../../docs/start/list-of-operations.md#manage-buy-offer).

 - OpSuccess - MANAGE\_BUY\_OFFER\_SUCCESS - The offer was successfully placed. - OpMalformed - MANAGE\_BUY\_OFFER\_MALFORMED - The input is incorrect and would result in an invalid offer. - op\_sell\_no\_trust - MANAGE\_BUY\_OFFER\_SELL\_NO\_TRUST - The account creating the offer does not have a trustline for the asset it is selling. - op\_buy\_no\_trust - MANAGE\_BUY\_OFFER\_BUY\_NO\_TRUST - The account creating the offer does not have a trustline for the asset it is buying. - sell\_not\_authorized - MANAGE\_BUY\_OFFER\_SELL\_NOT\_AUTHORIZED - The account creating the offer is not authorized to sell this asset. - buy\_not\_authorized - MANAGE\_BUY\_OFFER\_BUY\_NOT\_AUTHORIZED - The account creating the offer is not authorized to buy this asset. - OpLineFull - MANAGE\_BUY\_OFFER\_LINE\_FULL - The account creating the offer does not have sufficient limits to receive buying and still satisfy its buying liabilities. - OpUnderfunded - MANAGE\_BUY\_OFFER\_UNDERFUNDED - The account creating the offer does not have sufficient limits to send selling and still satisfy its selling liabilities. Note that if selling XLM then the account must additionally maintain its minimum XLM reserve, which is calculated assuming this offer will not completely execute immediately. - op\_cross\_self - MANAGE\_BUY\_OFFER\_CROSS\_SELF - The account has opposite offer of equal or lesser price active, so the account creating this offer would immediately cross itself. - op\_sell\_no\_issuer - MANAGE\_BUY\_OFFER\_SELL\_NO\_ISSUER - The issuer of selling asset does not exist. - buy\_no\_issuer - MANAGE\_BUY\_OFFER\_BUY\_NO\_ISSUER - The issuer of buying asset does not exist. - op\_offer\_not\_found - MANAGE\_BUY\_OFFER\_NOT\_FOUND - An offer with that offerID cannot be found. - OpLowReserve - MANAGE\_BUY\_OFFER\_LOW\_RESERVE - The account creating this offer does not have enough XLM to satisfy the minimum XLM reserve increase caused by adding a subentry and still satisfy its XLM selling liabilities. For every offer an account creates, the minimum amount of XLM that account must hold will increase.

