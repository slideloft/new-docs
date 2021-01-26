---
title: List All Ledgers
order: 60
---

# list

import { Endpoint } from "components/Endpoint"; import { ExampleResponse } from "components/ExampleResponse"; import { CodeExample } from "components/CodeExample"; import { AttributeTable } from "components/AttributeTable";

This endpoint lists all ledgers and can be used in [streaming](../../introduction/streaming.md) mode.

Streaming mode allows you to listen for new ledgers as they close. If called in streaming mode, Horizon will start at the earliest known ledger unless a `cursor` is set, in which case it will start from that `cursor`. By setting the cursor value to `now`, you can stream ledgers since your request time.

 \| \| \| \| --- \| --- \| \| GET \| /ledgers?&cursor={paging\_token}&order={asc,desc}&limit={1-200} \|

 - ARGUMENT - REQUIRED - DESCRIPTION - cursor - string \(optional\) - A number that points to a specific location in a collection of responses and is pulled from the \`paging\_token\` value of a record. - order - string \(optional\) - A designation of the order in which records should appear. Options include \`asc\`\(ascending\) or \`desc\` \(descending\). If this argument isn’t set, it defaults to \`asc\`. - limit - integer \(optional\) - The total number of records returned. The limit can range from 1 to 200 - an upper limit that is hardcoded in Horizon for performance reasons. If this argument isn’t designated, it defaults to 10.

 \`\`\`curl curl "https://horizon-testnet.stellar.org/ledgers?limit=200&order=desc" \`\`\` \`\`\`js var StellarSdk = require\("stellar-sdk"\); var server = new StellarSdk.Server\("https://horizon.stellar.org"\); server .ledgers\(\) .call\(\) .then\(function \(ledgerResult\) { // page 1 console.log\(ledgerResult.records\) return ledgerResult.next\(\) }\) .then\(function \(ledgerResult\) { // page 2 console.log\(ledgerResult.records\) }\) .catch\(function\(err\) { console.log\(err\) }\); \`\`\`

 \`\`\`json { "\_embedded": { "records": \[ { "\_links": { "effects": { "href": "/ledgers/1/effects/{?cursor,limit,order}", "templated": true }, "operations": { "href": "/ledgers/1/operations/{?cursor,limit,order}", "templated": true }, "self": { "href": "/ledgers/1" }, "transactions": { "href": "/ledgers/1/transactions/{?cursor,limit,order}", "templated": true } }, "id": "e8e10918f9c000c73119abe54cf089f59f9015cc93c49ccf00b5e8b9afb6e6b1", "paging\_token": "4294967296", "hash": "e8e10918f9c000c73119abe54cf089f59f9015cc93c49ccf00b5e8b9afb6e6b1", "sequence": 1, "transaction\_count": 0, "successful\_transaction\_count": 0, "failed\_transaction\_count": 0, "operation\_count": 0, "tx\_set\_operation\_count": 0, "closed\_at": "1970-01-01T00:00:00Z", "total\_coins": "100000000000.0000000", "fee\_pool": "0.0000000", "base\_fee\_in\_stroops": 100, "base\_reserve\_in\_stroops": 100000000, "max\_tx\_set\_size": 50 }, { "\_links": { "effects": { "href": "/ledgers/2/effects/{?cursor,limit,order}", "templated": true }, "operations": { "href": "/ledgers/2/operations/{?cursor,limit,order}", "templated": true }, "self": { "href": "/ledgers/2" }, "transactions": { "href": "/ledgers/2/transactions/{?cursor,limit,order}", "templated": true } }, "id": "e12e5809ab8c59d8256e691cb48a024dd43960bc15902d9661cd627962b2bc71", "paging\_token": "8589934592", "hash": "e12e5809ab8c59d8256e691cb48a024dd43960bc15902d9661cd627962b2bc71", "prev\_hash": "e8e10918f9c000c73119abe54cf089f59f9015cc93c49ccf00b5e8b9afb6e6b1", "sequence": 2, "transaction\_count": 0, "successful\_transaction\_count": 0, "failed\_transaction\_count": 0, "operation\_count": 0, "closed\_at": "2015-07-16T23:49:00Z", "total\_coins": "100000000000.0000000", "fee\_pool": "0.0000000", "base\_fee\_in\_stroops": 100, "base\_reserve\_in\_stroops": 100000000, "max\_tx\_set\_size": 100 } \] }, "\_links": { "next": { "href": "/ledgers?order=asc&limit=2&cursor=8589934592" }, "prev": { "href": "/ledgers?order=desc&limit=2&cursor=4294967296" }, "self": { "href": "/ledgers?order=asc&limit=2&cursor=" } } } \`\`\`

 \`\`\`js var StellarSdk = require\("stellar-sdk"\); var server = new StellarSdk.Server\("https://horizon.stellar.org"\); var callback = function \(resp\) { console.log\(resp\); }; var ledgerHandler = function \(ledgerResponse\) { console.log\(ledgerResponse\); }; var es = server.ledgers\(\) .cursor\('now'\) .stream\({ onmessage: ledgerHandler }\); \`\`\`

