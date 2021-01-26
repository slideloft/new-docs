---
title: Claim Claimable Balance
order: 150
---

# claim-claimable-balance

import { ExampleResponse } from "components/ExampleResponse"; import { AttributeTable } from "components/AttributeTable";

Claims a claimable balance.

 - ATTRIBUTE - DATA TYPE - DESCRIPTION - balance\_id - string - The id of the claimable balance. - claimant - string - The id of the account which claimed the balance.

 \`\`\`json { "\_links": { "self": { "href": "https://horizon.stellar.org/operations/124922916260433921" }, "transaction": { "href": "https://horizon.stellar.org/transactions/f94c338370839a598753221714de0b0193d4fc56ea369db6efe88f18669cc5a1" }, "effects": { "href": "https://horizon.stellar.org/operations/124922916260433921/effects" }, "succeeds": { "href": "https://horizon.stellar.org/effects?order=desc\u0026cursor=124922916260433921" }, "precedes": { "href": "https://horizon.stellar.org/effects?order=asc\u0026cursor=124922916260433921" } }, "id": "124922916260433921", "paging\_token": "124922916260433921", "transaction\_successful": true, "source\_account": "GAYOLLLUIZE4DZMBB2ZBKGBUBZLIOYU6XFLW37GBP2VZD3ABNXCW4BVA", "type": "claim\_claimable\_balance", "type\_i": 15, "created\_at": "2020-04-09T00:14:11Z", "transaction\_hash": "f94c338370839a598753221714de0b0193d4fc56ea369db6efe88f18669cc5a1", "id": "000000000102030000000000000000000000000000000000000000000000000000000000", "claimant": "GC3C4AKRBQLHOJ45U4XG35ESVWRDECWO5XLDGYADO6DPR3L7KIDVUMML" } \`\`\`

