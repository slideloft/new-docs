---
title: Manage Buy Offer Object
order: 60
---

# buy-offer

import { ExampleResponse } from "components/ExampleResponse"; import { AttributeTable } from "components/AttributeTable";

Creates, updates, or deletes a buy offer to trade assets. A buy offer specifies a certain amount of the buying asset that should be sold in exchange for the minimum quantity of the selling asset.

See the [`Manage Buy Offer` errors](../../../errors/result-codes/operation-specific/manage-buy-offer.md).

 - ATTRIBUTE - DATA TYPE - DESCRIPTION - amount - string - The amount of \`buying\_asset\` that the account making this offer is willing to buy. - price - string - How many units of \`buying\_asset\` it takes to get 1 unit of \`selling\_asset\`. A number representing the decimal form of \`price\_r\`. - price\_r - object - A precise representation of the buy and sell price of the assets on offer. - n - number - The numerator. - d - number - The denominator. - buying\_asset\_type - string - The type for the buying asset. Either \`native\`, \`credit\_alphanum4\`, or \`credit\_alphanum12\`. - buying\_asset\_issuer - string - The Stellar address of the buying asset’s issuer. Appears if the \`buying\_asset\_type\` is not \`native\`. - buying\_asset\_code - string - The code for the buying asset. Appears if the \`buying\_asset\_type\` is not \`native\`. - selling\_asset\_type - string - The type for the selling asset. Either \`native\`, \`credit\_alphanum4\`, or \`credit\_alphanum12\`. - selling\_asset\_issuer - string - The Stellar address of the selling asset’s issuer. Appears if the \`selling\_asset\_type\` is not \`native\`. - selling\_asset\_code - string - The code for the selling asset. Appears if the \`selling\_asset\_type\` is not \`native\`. - offer\_id - string - A unique identifier for this offer.

 \`\`\`json { "\_links": { "self": { "href": "https://horizon.stellar.org/operations/124893981065674756" }, "transaction": { "href": "https://horizon.stellar.org/transactions/3b41ec1411ed67ed47c96c34067c9fcfadf6e7cc013effa0b10f3df5ed758ffc" }, "effects": { "href": "https://horizon.stellar.org/operations/124893981065674756/effects" }, "succeeds": { "href": "https://horizon.stellar.org/effects?order=desc\u0026cursor=124893981065674756" }, "precedes": { "href": "https://horizon.stellar.org/effects?order=asc\u0026cursor=124893981065674756" } }, "id": "124893981065674756", "paging\_token": "124893981065674756", "transaction\_successful": true, "source\_account": "GDT7WYNV6YBFJH3G6TX5K3ALBZY7A7A7CLIGXK4XZ6H5SROPS4UFGEMC", "type": "manage\_buy\_offer", "type\_i": 12, "created\_at": "2020-04-08T14:03:03Z", "transaction\_hash": "3b41ec1411ed67ed47c96c34067c9fcfadf6e7cc013effa0b10f3df5ed758ffc", "amount": "20.4521401", "price": "0.0300003", "price\_r": { "n": 9000190, "d": 300003333 }, "buying\_asset\_type": "native", "selling\_asset\_type": "credit\_alphanum4", "selling\_asset\_code": "EURT", "selling\_asset\_issuer": "GAP5LETOV6YIE62YAM56STDANPRDO7ZFDBGSNHJQIYGGKSMOZAHOOS2S", "offer\_id": "0" } \`\`\`

