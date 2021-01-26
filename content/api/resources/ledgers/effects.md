---
title: Retrieve a Ledgers's Effects
order: 50
---

# effects

import { Endpoint } from "components/Endpoint"; import { ExampleResponse } from "components/ExampleResponse"; import { CodeExample } from "components/CodeExample"; import { AttributeTable } from "components/AttributeTable";

This endpoint returns the effects of a specific ledger.

 \| \| \| \| --- \| --- \| \| GET \| /ledgers/:ledger\_sequence/effects?cursor={paging\_token}&order={asc,desc}&limit={1-200} \|

 - ARGUMENT - REQUIRED - DESCRIPTION - ledger\_sequence - required - The sequence number of a specific ledger. - cursor - optional - A number that points to a specific location in a collection of responses and is pulled from the \`paging\_token\` value of a record. - order - optional - A designation of the order in which records should appear. Options include \`asc\`\(ascending\) or \`desc\` \(descending\). If this argument isn’t set, it defaults to \`asc\`. - limit - optional - The total number of records returned. The limit can range from 1 to 200 - an upper limit that is hardcoded in Horizon for performance reasons. If this argument isn’t designated, it defaults to 10.

 \`\`\`curl curl "https://horizon.stellar.org/ledgers/0/effects" \`\`\` \`\`\`js var StellarSdk = require\("stellar-sdk"\); var server = new StellarSdk.Server\("https://horizon.stellar.org"\); server .effects\(\) .forLedger\(0\) .call\(\) .then\(function \(resp\) { console.log\(resp\); }\) .catch\(function \(err\) { console.error\(err\); }\); \`\`\`

 \`\`\`json { "\_links": { "self": { "href": "https://horizon.stellar.org/ledgers/0/effects?cursor=&limit=10&order=asc" }, "next": { "href": "https://horizon.stellar.org/ledgers/0/effects?cursor=33676838572034-1&limit=10&order=asc" }, "prev": { "href": "https://horizon.stellar.org/ledgers/0/effects?cursor=12884905985-1&limit=10&order=desc" } }, "\_embedded": { "records": \[ { "\_links": { "operation": { "href": "https://horizon.stellar.org/operations/12884905985" }, "succeeds": { "href": "https://horizon.stellar.org/effects?order=desc&cursor=12884905985-1" }, "precedes": { "href": "https://horizon.stellar.org/effects?order=asc&cursor=12884905985-1" } }, "id": "0000000012884905985-0000000001", "paging\_token": "12884905985-1", "account": "GALPCCZN4YXA3YMJHKL6CVIECKPLJJCTVMSNYWBTKJW4K5HQLYLDMZTB", "type": "account\_created", "type\_i": 0, "created\_at": "2015-09-30T17:15:54Z", "starting\_balance": "20.0000000" }, { "\_links": { "operation": { "href": "https://horizon.stellar.org/operations/12884905985" }, "succeeds": { "href": "https://horizon.stellar.org/effects?order=desc&cursor=12884905985-2" }, "precedes": { "href": "https://horizon.stellar.org/effects?order=asc&cursor=12884905985-2" } }, "id": "0000000012884905985-0000000002", "paging\_token": "12884905985-2", "account": "GAAZI4TCR3TY5OJHCTJC2A4QSY6CJWJH5IAJTGKIN2ER7LBNVKOCCWN7", "type": "account\_debited", "type\_i": 3, "created\_at": "2015-09-30T17:15:54Z", "asset\_type": "native", "amount": "20.0000000" } \] } } \`\`\`

