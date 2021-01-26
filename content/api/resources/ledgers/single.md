---
title: Retrieve a Ledger
order: 20
---

# single

import { Endpoint } from "components/Endpoint"; import { ExampleResponse } from "components/ExampleResponse"; import { CodeExample } from "components/CodeExample"; import { AttributeTable } from "components/AttributeTable";

The single ledger endpoint provides information on a specific ledger.

 \| \| \| \| --- \| ------------------------- \| \| GET \| /ledgers/:ledger\_sequence \|

 - ARGUMENT - REQUIRED - DESCRIPTION - sequence - required - The sequence number of a specific ledger.

 \`\`\`curl curl "https://horizon.stellar.org/ledgers/69859" \`\`\` \`\`\`js var StellarSdk = require\("stellar-sdk"\); var server = new StellarSdk.Server\("https://horizon.stellar.org"\); server .ledgers\(\) .ledger\("69858"\) .call\(\) .then\(function \(resp\) { console.log\(resp\); }\) .catch\(function \(err\) { console.error\(err\); }\); \`\`\`

 \`\`\`json "\_links": { "self": { "href": "https://horizon.stellar.org/ledgers/27146933" }, "transactions": { "href": "https://horizon.stellar.org/ledgers/27146933/transactions{?cursor,limit,order}", "templated": true }, "operations": { "href": "https://horizon.stellar.org/ledgers/27146933/operations{?cursor,limit,order}", "templated": true }, "payments": { "href": "https://horizon.stellar.org/ledgers/27146933/payments{?cursor,limit,order}", "templated": true }, "effects": { "href": "https://horizon.stellar.org/ledgers/27146933/effects{?cursor,limit,order}", "templated": true } }, "id": "e1218a337cecda05526fba902c61d3d7130baa58d8db41f544bf563f779b6329", "paging\_token": "116595189421703168", "hash": "e1218a337cecda05526fba902c61d3d7130baa58d8db41f544bf563f779b6329", "prev\_hash": "9eac16fecd885147067b58b7684f60d216f931b813f651265bbc97de4cea313d", "sequence": 27146933, "successful\_transaction\_count": 26, "failed\_transaction\_count": 9, "operation\_count": 67, "closed\_at": "2019-12-06T22:39:32Z", "total\_coins": "105443902087.3472865", "fee\_pool": "1807264.7509661", "base\_fee\_in\_stroops": 100, "base\_reserve\_in\_stroops": 5000000, "max\_tx\_set\_size": 1000, "protocol\_version": 12, "header\_xdr": "AAAADJ6sFv7NiFFHBntYt2hPYNIW+TG4E/ZRJlu8l95M6jE9bsvzId+Gtul2mNMW4UZQ+KqSb/nbN8F1CTxAfQsyUy8AAAAAXerYpAAAAAAAAAAAXQNpS8daKGZUeY5quYUcIiJZBMB7LiLsZJsEx9qw79fx99Bu/lk+sIePNUNcuOC2euthzfhLuWJ1nZBuoQFDjgGeOrUOoh6z7HlbYQAAEG/dvCadAAABFgAAAAAIOwAqAAAAZABMS0AAAAPooSNtHXJNJKKWlBtgkAM1LBxzlzYjIlS0xwpjP+uCi76fQj59wgTy0+xtx7O1qTb+W6zcI2zWZnrUU/8v8RZHFBfoo20QYKh95+wWr348yZAexZpdrjhyCxbChxlVTZOX6nZfIgcYBMnZRkOTCLdPO76yeqpDhqu9KrPe3YPTO3wAAAAA" } \`\`\`

