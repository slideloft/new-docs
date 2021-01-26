---
title: Manage Sell Offer Object
order: 50
---

# sell-offer

import { ExampleResponse } from "components/ExampleResponse"; import { AttributeTable } from "components/AttributeTable";

Creates, updates, or deletes a sell offer to trade assets. A sell offer specifies a certain amount of the selling asset that should be sold in exchange for the maximum quantity of the buying asset.

See the [`Manage Sell Offer` errors](../../../errors/result-codes/operation-specific/manage-sell-offer.md).

 - ATTRIBUTE - DATA TYPE - DESCRIPTION - amount - string - The amount of \`selling\_asset\` that the account making this offer is willing to sell. - price - string - How many units of \`selling\_asset\` it takes to get 1 unit of \`buying\_asset\`. A number representing the decimal form of \`price\_r\`. - price\_r - object - A precise representation of the buy and sell price of the assets on offer. - n - number - The numerator. - d - number - The denominator. - buying\_asset\_type - string - The type for the buying asset. Either \`native\`, \`credit\_alphanum4\`, or \`credit\_alphanum12\`. - buying\_asset\_issuer - string - The Stellar address of the buying asset’s issuer. Appears if the \`buying\_asset\_type\` is not \`native\`. - buying\_asset\_code - string - The code for the buying asset. Appears if the \`buying\_asset\_type\` is not \`native\`. - selling\_asset\_type - string - The type for the selling asset. Either \`native\`, \`credit\_alphanum4\`, or \`credit\_alphanum12\`. - selling\_asset\_issuer - string - The Stellar address of the selling asset’s issuer. Appears if the \`selling\_asset\_type\` is not \`native\`. - selling\_asset\_code - string - The code for the selling asset. Appears if the \`selling\_asset\_type\` is not \`native\`. - offer\_id - string - A unique identifier for this offer.

 \`\`\`json { "\_links": { "self": { "href": "https://horizon.stellar.org/operations/124892722640347138" }, "transaction": { "href": "https://horizon.stellar.org/transactions/ef8ffb54ff5990a686fda3ebfc07b8162f042ff0fcdb4f7ff141531e386f0a18" }, "effects": { "href": "https://horizon.stellar.org/operations/124892722640347138/effects" }, "succeeds": { "href": "https://horizon.stellar.org/effects?order=desc\u0026cursor=124892722640347138" }, "precedes": { "href": "https://horizon.stellar.org/effects?order=asc\u0026cursor=124892722640347138" } }, "id": "124892722640347138", "paging\_token": "124892722640347138", "transaction\_successful": true, "source\_account": "GCM4PT6XDZBWOOENDS6FOU22GJQLJPV2GC7VRVII4TFGZBA3ZXNM55SV", "type": "manage\_sell\_offer", "type\_i": 3, "created\_at": "2020-04-08T13:36:39Z", "transaction\_hash": "ef8ffb54ff5990a686fda3ebfc07b8162f042ff0fcdb4f7ff141531e386f0a18", "amount": "1336.0326986", "price": "0.0559999", "price\_r": { "n": 559999, "d": 10000000 }, "buying\_asset\_type": "credit\_alphanum4", "buying\_asset\_code": "USD", "buying\_asset\_issuer": "GDUKMGUGDZQK6YHYA5Z6AY2G4XDSZPSZ3SW5UN3ARVMO6QSRDWP5YLEX", "selling\_asset\_type": "native", "offer\_id": "0" } \`\`\`

