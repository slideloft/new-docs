---
title: Retrieve an Operation's Effects
order: 30
---

# effects

import { Endpoint } from "components/Endpoint"; import { ExampleResponse } from "components/ExampleResponse"; import { CodeExample } from "components/CodeExample"; import { AttributeTable } from "components/AttributeTable";

This endpoint returns the effects of a specific operation.

 \| \| \| \| --- \| --- \| \| GET \| /operations/:operation\_id/effects?cursor={paging\_token}&order={asc,desc}&limit={1-200} \|

 - ARGUMENT - REQUIRED - DESCRIPTION - id - required - The ID number for this operation. - cursor - optional - A number that points to a specific location in a collection of responses and is pulled from the \`paging\_token\` value of a record. - order - optional - A designation of the order in which records should appear. Options include \`asc\`\(ascending\) or \`desc\` \(descending\). If this argument isn’t set, it defaults to \`asc\`. - limit - optional - The total number of records returned. The limit can range from 1 to 200 - an upper limit that is hardcoded in Horizon for performance reasons. If this argument isn’t designated, it defaults to 10.

 \`\`\`curl curl "https://horizon.stellar.org/operations/121693057904021505/effects" \`\`\` \`\`\`js var StellarSdk = require\("stellar-sdk"\); var server = new StellarSdk.Server\("https://horizon.stellar.org"\); server .effects\(\) .forOperation\("121693057904021505"\) .call\(\) .then\(function \(resp\) { console.log\(resp\); }\) .catch\(function \(err\) { console.error\(err\); }\); \`\`\`

 \`\`\`json { "\_links": { "self": { "href": "https://horizon.stellar.org/operations/121693057904021505/effects?cursor=\u0026limit=10\u0026order=asc" }, "next": { "href": "https://horizon.stellar.org/operations/121693057904021505/effects?cursor=121693057904021505-2\u0026limit=10\u0026order=asc" }, "prev": { "href": "https://horizon.stellar.org/operations/121693057904021505/effects?cursor=121693057904021505-1\u0026limit=10\u0026order=desc" } }, "\_embedded": { "records": \[ { "\_links": { "operation": { "href": "https://horizon.stellar.org/operations/121693057904021505" }, "succeeds": { "href": "https://horizon.stellar.org/effects?order=desc\u0026cursor=121693057904021505-1" }, "precedes": { "href": "https://horizon.stellar.org/effects?order=asc\u0026cursor=121693057904021505-1" } }, "id": "0121693057904021505-0000000001", "paging\_token": "121693057904021505-1", "account": "GALSPNVKGNRJ3VIOQ26QKPZBDCTVJK7XPLSPF3UVZV3JJXCKVCHNSPCK", "type": "account\_credited", "type\_i": 2, "created\_at": "2020-02-21T20:27:30Z", "asset\_type": "credit\_alphanum4", "asset\_code": "NODL", "asset\_issuer": "GB2Y3AWXVROM2BHFQKQPTWKIOI3TZEBBD3LTKTVQTKEPXGOBE742NODL", "amount": "0.0000027" }, { "\_links": { "operation": { "href": "https://horizon.stellar.org/operations/121693057904021505" }, "succeeds": { "href": "https://horizon.stellar.org/effects?order=desc\u0026cursor=121693057904021505-2" }, "precedes": { "href": "https://horizon.stellar.org/effects?order=asc\u0026cursor=121693057904021505-2" } }, "id": "0121693057904021505-0000000002", "paging\_token": "121693057904021505-2", "account": "GDQWI6FKB72DPOJE4CGYCFQZKRPQQIOYXRMZ5KEVGXMG6UUTGJMBCASH", "type": "account\_debited", "type\_i": 3, "created\_at": "2020-02-21T20:27:30Z", "asset\_type": "credit\_alphanum4", "asset\_code": "NODL", "asset\_issuer": "GB2Y3AWXVROM2BHFQKQPTWKIOI3TZEBBD3LTKTVQTKEPXGOBE742NODL", "amount": "0.0000027" } \] } } \`\`\`

