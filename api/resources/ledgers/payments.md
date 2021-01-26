---
title: Retrieve a Ledger's Payments
order: 40
---

# payments

import { Endpoint } from "components/Endpoint"; import { ExampleResponse } from "components/ExampleResponse"; import { CodeExample } from "components/CodeExample"; import { AttributeTable } from "components/AttributeTable";

This endpoint returns all payment-related operations in a specific ledger.

Operation types that can be returned by this endpoint include:

* `create_account`
* `payment`
* `path_payment`
* `account_merge`

 \| \| \| \| --- \| --- \| \| GET \| /ledgers/:ledger\_sequence/payments?cursor={paging\_token}&order={asc,desc}&limit={1-200}&include\_failed{true,false}&join={transactions} \|

 - ARGUMENT - REQUIRED - DESCRIPTION - ledger\_sequence - required - The sequence number of a specific ledger. - cursor - optional - A number that points to a specific location in a collection of responses and is pulled from the \`paging\_token\` value of a record. - order - optional - A designation of the order in which records should appear. Options include \`asc\`\(ascending\) or \`desc\` \(descending\). If this argument isn’t set, it defaults to \`asc\`. - limit - optional - The total number of records returned. The limit can range from 1 to 200 - an upper limit that is hardcoded in Horizon for performance reasons. If this argument isn’t designated, it defaults to 10. - include\_failed - optional - Set to true to include failed payments in results. Options include \`true\` and \`false\`. - join - optional - Set to \`transactions\` to include the transactions which created each of the payments in the response.

 \`\`\`curl curl "https://horizon.stellar.org/ledgers/27521176/payments?limit=1" \`\`\` \`\`\`js var StellarSdk = require\("stellar-sdk"\); var server = new StellarSdk.Server\("https://horizon.stellar.org"\); server .payments\(\) .forLedger\("27521176"\) .call\(\) .then\(function \(resp\) { console.log\(resp\); }\) .catch\(function \(err\) { console.error\(err\); }\); \`\`\`

 \`\`\`json { "\_links": { "self": { "href": "https://horizon.stellar.org/ledgers/27521176/payments?cursor=\u0026limit=1\u0026order=asc" }, "next": { "href": "https://horizon.stellar.org/ledgers/27521176/payments?cursor=118202550867476481\u0026limit=1\u0026order=asc" }, "prev": { "href": "https://horizon.stellar.org/ledgers/27521176/payments?cursor=118202550867476481\u0026limit=1\u0026order=desc" } }, "\_embedded": { "records": \[ { "\_links": { "self": { "href": "https://horizon.stellar.org/operations/118202550867476481" }, "transaction": { "href": "https://horizon.stellar.org/transactions/971454b84a82baa38afa975e9eb4ff2632821b5a3e7f7993a7e20bbd9d7633ea" }, "effects": { "href": "https://horizon.stellar.org/operations/118202550867476481/effects" }, "succeeds": { "href": "https://horizon.stellar.org/effects?order=desc\u0026cursor=118202550867476481" }, "precedes": { "href": "https://horizon.stellar.org/effects?order=asc\u0026cursor=118202550867476481" } }, "id": "118202550867476481", "paging\_token": "118202550867476481", "transaction\_successful": true, "source\_account": "GDQWI6FKB72DPOJE4CGYCFQZKRPQQIOYXRMZ5KEVGXMG6UUTGJMBCASH", "type": "payment", "type\_i": 1, "created\_at": "2019-12-30T22:35:49Z", "transaction\_hash": "971454b84a82baa38afa975e9eb4ff2632821b5a3e7f7993a7e20bbd9d7633ea", "asset\_type": "credit\_alphanum4", "asset\_code": "NODL", "asset\_issuer": "GB2Y3AWXVROM2BHFQKQPTWKIOI3TZEBBD3LTKTVQTKEPXGOBE742NODL", "from": "GDQWI6FKB72DPOJE4CGYCFQZKRPQQIOYXRMZ5KEVGXMG6UUTGJMBCASH", "to": "GDGJS7AXAUFDZARIRDVZ5V7CFW6XY47WSBE2OVLCCGCDWOE7INKYN3PS", "amount": "0.0000017" } \] } } \`\`\`

