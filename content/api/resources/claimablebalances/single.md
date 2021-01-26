---
title: Retrieve a Claimable Balance
order: 20
---

# single

import { Endpoint } from "components/Endpoint"; import { ExampleResponse } from "components/ExampleResponse"; import { CodeExample } from "components/CodeExample"; import { AttributeTable } from "components/AttributeTable";

The single claimable balance endpoint provides information on a claimable balance.

 \| \| \| \| --- \| ----------------------------------------- \| \| GET \| /claimable\_balances/:claimable\_balance\_id \|

 - ARGUMENT - REQUIRED - DESCRIPTION - claimable\_balance\_id - required - A unique identifier for this claimable balance.

 \`\`\`curl curl "https://horizon.stellar.org/claimable\_balances/000000000102030000000000000000000000000000000000000000000000000000000000" \`\`\` \`\`\`js var StellarSdk = require\("stellar-sdk"\); var server = new StellarSdk.Server\("https://horizon.stellar.org"\); server .claimableBalances\(\) .claimableBalanceId\( "000000000102030000000000000000000000000000000000000000000000000000000000", \) .call\(\) .then\(function \(resp\) { console.log\(resp\); }\) .catch\(function \(err\) { console.error\(err\); }\); \`\`\`

 \`\`\`json { "\_links": { "self": { "href": "https://horizon.stellar.org/claimable\_balances/000000000102030000000000000000000000000000000000000000000000000000000000" } }, "id": "000000000102030000000000000000000000000000000000000000000000000000000000", "paging\_token": "000000000102030000000000000000000000000000000000000000000000000000000000", "asset": "native", "amount": "10.0000000", "claimants": \[ { "destination": "GC3C4AKRBQLHOJ45U4XG35ESVWRDECWO5XLDGYADO6DPR3L7KIDVUMML", "predicate": { { "and": \[ { "or": \[ { "relBefore": "12" }, { "absBefore": "2020-08-26T11:15:39Z" } \] }, { "not": {"unconditional": true} } \] } } } \], "last\_modified\_ledger": 28411995, "last\_modified\_time": "2020-02-26T19:29:16Z" } \`\`\`

