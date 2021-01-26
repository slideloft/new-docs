---
title: Create Passive Sell Offer Object
order: 70
---

# passive-sell-offer

import { ExampleResponse } from "components/ExampleResponse"; import { AttributeTable } from "components/AttributeTable";

Creates an offer that will not consume a counter offer that exactly matches this offer. This is useful for offers meant to be 1:1 exchanges for path payments. Use Manage Sell Offer to manage this offer after using this operation to create it.

See the [`Create Passive Sell Offer` errors](../../../errors/result-codes/operation-specific/create-passive-sell-offer.md).

 - ATTRIBUTE - DATA TYPE - DESCRIPTION - amount - string - The amount of \`selling\_asset\` that the account making this offer is willing to sell. - price - string - How many units of \`selling\_asset\` it takes to get 1 unit of \`buying\_asset\`. A number representing the decimal form of \`price\_r\`. - price\_r - object - A precise representation of the buy and sell price of the assets on offer. - n - number - The numerator. - d - number - The denominator. - buying\_asset\_type - string - The type for the buying asset. Either \`native\`, \`credit\_alphanum4\`, or \`credit\_alphanum12\`. - buying\_asset\_issuer - string - The Stellar address of the buying asset’s issuer. Appears if the \`buying\_asset\_type\` is not \`native\`. - buying\_asset\_code - string - The code for the buying asset. Appears if the \`buying\_asset\_type\` is not \`native\`. - selling\_asset\_type - string - The type for the selling asset. Either \`native\`, \`credit\_alphanum4\`, or \`credit\_alphanum12\`. - selling\_asset\_issuer - string - The Stellar address of the selling asset’s issuer. Appears if the \`selling\_asset\_type\` is not \`native\`. - selling\_asset\_code - string - The code for the selling asset. Appears if the \`selling\_asset\_type\` is not \`native\`. - offer\_id - string - A unique identifier for this offer.

 \`\`\`json { "\_links": { "self": { "href": "https://horizon.stellar.org/operations/124895183656849409" }, "transaction": { "href": "https://horizon.stellar.org/transactions/20afb7f9613efe9e851579190c80758ee101550e85740f71274c3eb3f0cb0418" }, "effects": { "href": "https://horizon.stellar.org/operations/124895183656849409/effects" }, "succeeds": { "href": "https://horizon.stellar.org/effects?order=desc\u0026cursor=124895183656849409" }, "precedes": { "href": "https://horizon.stellar.org/effects?order=asc\u0026cursor=124895183656849409" } }, "id": "124895183656849409", "paging\_token": "124895183656849409", "transaction\_successful": true, "source\_account": "GAYOLLLUIZE4DZMBB2ZBKGBUBZLIOYU6XFLW37GBP2VZD3ABNXCW4BVA", "type": "create\_passive\_sell\_offer", "type\_i": 4, "created\_at": "2020-04-08T14:28:15Z", "transaction\_hash": "20afb7f9613efe9e851579190c80758ee101550e85740f71274c3eb3f0cb0418", "amount": "1.0000000", "price": "1.0000000", "price\_r": { "n": 1, "d": 1 }, "buying\_asset\_type": "credit\_alphanum4", "buying\_asset\_code": "USD", "buying\_asset\_issuer": "GBNLJIYH34UWO5YZFA3A3HD3N76R6DOI33N4JONUOHEEYZYCAYTEJ5AK", "selling\_asset\_type": "credit\_alphanum4", "selling\_asset\_code": "USD", "selling\_asset\_issuer": "GDUKMGUGDZQK6YHYA5Z6AY2G4XDSZPSZ3SW5UN3ARVMO6QSRDWP5YLEX" } \`\`\`

