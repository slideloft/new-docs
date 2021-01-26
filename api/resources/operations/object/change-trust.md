---
title: Change Trust Object
order: 90
---

# change-trust

import { ExampleResponse } from "components/ExampleResponse"; import { AttributeTable } from "components/AttributeTable";

Creates, updates, or deletes a trust line from the source account to another account's issued asset.

See the [`Change Trust` errors](../../../errors/result-codes/operation-specific/change-trust.md).

 - ATTRIBUTE - DATA TYPE - DESCRIPTION - asset\_type - string - The type of asset being trusted. Either \`native\`, \`credit\_alphanum4\`, or \`credit\_alphanum12\`. - asset\_code - string - The Stellar address of the asset being trusted. - asset\_issuer - string - The code for the asset being trusted. - limit - string - Limits the amount of an asset that the source account can hold. - trustee - string - The issuing account. - trustor - string - The source account.

 \`\`\`json { "\_links": { "self": { "href": "https://horizon.stellar.org/operations/120192477935251457" }, "transaction": { "href": "https://horizon.stellar.org/transactions/ec4116595bdfa8c1039c40af425e497c91fcf387c2a2a0cfa1f3bf64733f1f23" }, "effects": { "href": "https://horizon.stellar.org/operations/120192477935251457/effects" }, "succeeds": { "href": "https://horizon.stellar.org/effects?order=desc\u0026cursor=120192477935251457" }, "precedes": { "href": "https://horizon.stellar.org/effects?order=asc\u0026cursor=120192477935251457" } }, "id": "120192477935251457", "paging\_token": "120192477935251457", "transaction\_successful": true, "source\_account": "GAYOLLLUIZE4DZMBB2ZBKGBUBZLIOYU6XFLW37GBP2VZD3ABNXCW4BVA", "type": "change\_trust", "type\_i": 6, "created\_at": "2020-01-29T19:46:55Z", "transaction\_hash": "ec4116595bdfa8c1039c40af425e497c91fcf387c2a2a0cfa1f3bf64733f1f23", "asset\_type": "credit\_alphanum4", "asset\_code": "NGNT", "asset\_issuer": "GAWODAROMJ33V5YDFY3NPYTHVYQG7MJXVJ2ND3AOGIHYRWINES6ACCPD", "limit": "922337203685.4775807", "trustee": "GAWODAROMJ33V5YDFY3NPYTHVYQG7MJXVJ2ND3AOGIHYRWINES6ACCPD", "trustor": "GAYOLLLUIZE4DZMBB2ZBKGBUBZLIOYU6XFLW37GBP2VZD3ABNXCW4BVA" } \`\`\`

