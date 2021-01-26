---
title: Retrieve an Operation
order: 20
---

# single

import { Endpoint } from "components/Endpoint"; import { ExampleResponse } from "components/ExampleResponse"; import { CodeExample } from "components/CodeExample"; import { AttributeTable } from "components/AttributeTable";

The single operation endpoint provides information about a specific operation.

 \| \| \| \| --- \| ------------------------- \| \| GET \| /operations/:operation\_id \|

 - ARGUMENT - REQUIRED - DESCRIPTION - id - required - The ID number for this operation. - join - optional - Set to \`transactions\` to include the transactions which created each of the operations in the response.

 \`\`\`curl curl "https://horizon.stellar.org/operations/121692259040116737" \`\`\` \`\`\`js var StellarSdk = require\("stellar-sdk"\); var server = new StellarSdk.Server\("https://horizon.stellar.org"\); server .operations\(\) .operation\("121692259040116737"\) .call\(\) .then\(function \(resp\) { console.log\(resp\); }\) .catch\(function \(err\) { console.error\(err\); }\); \`\`\`

 \`\`\`json { "\_links": { "self": { "href": "https://horizon.stellar.org/operations/121692259040116737" }, "transaction": { "href": "https://horizon.stellar.org/transactions/f92a9648c1084d1de0fd786faac5d5e1637d4127c60841d2366c70d2e7f77b85" }, "effects": { "href": "https://horizon.stellar.org/operations/121692259040116737/effects" }, "succeeds": { "href": "https://horizon.stellar.org/effects?order=desc\u0026cursor=121692259040116737" }, "precedes": { "href": "https://horizon.stellar.org/effects?order=asc\u0026cursor=121692259040116737" } }, "id": "121692259040116737", "paging\_token": "121692259040116737", "transaction\_successful": true, "source\_account": "GBDVKE33GVVMBXX73OHIBRP6RAHKHHW2P4PQVV6UNOKQCOXU7GNUM4QI", "type": "manage\_offer", "type\_i": 3, "created\_at": "2020-02-21T20:10:21Z", "transaction\_hash": "f92a9648c1084d1de0fd786faac5d5e1637d4127c60841d2366c70d2e7f77b85", "amount": "10000.0000000", "price": "0.0704336", "price\_r": { "n": 44021, "d": 625000 }, "buying\_asset\_type": "credit\_alphanum4", "buying\_asset\_code": "USD", "buying\_asset\_issuer": "GDUKMGUGDZQK6YHYA5Z6AY2G4XDSZPSZ3SW5UN3ARVMO6QSRDWP5YLEX", "selling\_asset\_type": "native", "offer\_id": 161536436 } \`\`\`

