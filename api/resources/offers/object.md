---
title: The Offer Object
order: 10
---

# object

import { ExampleResponse } from "components/ExampleResponse"; import { AttributeTable } from "components/AttributeTable";

When Horizon returns information about an offer, it uses the following format:

 - ATTRIBUTE - DATA TYPE - DESCRIPTION - id - string - A unique identifier for this offer. - paging\_token - number - A cursor value for use in \[pagination\]\(../../introduction/pagination/index.mdx\). - seller - string - The account ID of the account making this offer. - selling - asset code - The asset this offer wants to sell. - buying - asset code - The asset this offer wants to buy. - amount - string - The amount of \`selling\` that the account making this offer is willing to sell. - price\_r - object - A precise representation of the buy and sell price of the assets on offer. - n - number - The numerator. - d - number - The denominator. - price - string - How many units of \`buying\` it takes to get 1 unit of \`selling\`. A number representing the decimal form of \`price\_r\`. - last\_modified\_ledger - integer - The sequence number of the last ledger in which this offer was modified. - last\_modified\_time - string - An ISO 8601 formatted string of last modification time. - sponsor - string \(optional\) - The account id of the sponsor who is paying the reserves for this offer.

 \`\`\`json { "\_links": { "self": { "href": "https://horizon.stellar.org/offers/165561423" }, "offer\_maker": { "href": "https://horizon.stellar.org/accounts/GCK4WSNF3F6ZNCMK6BU77ZCZ3NMF3JGU2U3ZAPKXYBKYYCJA72FDBY7K" } }, "id": 165561423, "paging\_token": "165561423", "seller": "GCK4WSNF3F6ZNCMK6BU77ZCZ3NMF3JGU2U3ZAPKXYBKYYCJA72FDBY7K", "selling": { "asset\_type": "credit\_alphanum4", "asset\_code": "NGNT", "asset\_issuer": "GAWODAROMJ33V5YDFY3NPYTHVYQG7MJXVJ2ND3AOGIHYRWINES6ACCPD" }, "buying": { "asset\_type": "native" }, "amount": "18421.4486092", "price\_r": { "n": 45112058, "d": 941460545 }, "price": "0.0479171", "last\_modified\_ledger": 28411995, "last\_modified\_time": "2020-02-26T19:29:16Z" } \`\`\`

