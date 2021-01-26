---
title: Retrieve an Offer
order: 20
---

# single

import { Endpoint } from "components/Endpoint"; import { ExampleResponse } from "components/ExampleResponse"; import { CodeExample } from "components/CodeExample"; import { AttributeTable } from "components/AttributeTable";

The single offer endpoint provides information on a specific offer.

 \| \| \| \| --- \| ----------------- \| \| GET \| /offers/:offer\_id \|

 - ARGUMENT - REQUIRED - DESCRIPTION - offer\_id - required - A unique identifier for this offer.

 \`\`\`curl curl "https://horizon.stellar.org/offers/165563085" \`\`\` \`\`\`js var StellarSdk = require\("stellar-sdk"\); var server = new StellarSdk.Server\("https://horizon.stellar.org"\); server .offers\(\) .offer\("165563085"\) .call\(\) .then\(function \(resp\) { console.log\(resp\); }\) .catch\(function \(err\) { console.error\(err\); }\); \`\`\`

 \`\`\`json { "\_links": { "self": { "href": "https://horizon.stellar.org/offers/165563085" }, "offer\_maker": { "href": "https://horizon.stellar.org/accounts/GCM4PT6XDZBWOOENDS6FOU22GJQLJPV2GC7VRVII4TFGZBA3ZXNM55SV" } }, "id": 165563085, "paging\_token": "165563085", "seller": "GCM4PT6XDZBWOOENDS6FOU22GJQLJPV2GC7VRVII4TFGZBA3ZXNM55SV", "selling": { "asset\_type": "credit\_alphanum4", "asset\_code": "USD", "asset\_issuer": "GDUKMGUGDZQK6YHYA5Z6AY2G4XDSZPSZ3SW5UN3ARVMO6QSRDWP5YLEX" }, "buying": { "asset\_type": "native" }, "amount": "26.1075388", "price\_r": { "n": 1449156725, "d": 84642346 }, "price": "17.1209423", "last\_modified\_ledger": 28412042, "last\_modified\_time": null } \`\`\`

