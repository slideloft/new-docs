---
title: Bump Sequence Object
order: 130
---

# bump-sequence

import { ExampleResponse } from "components/ExampleResponse"; import { AttributeTable } from "components/AttributeTable";

Bumps forward the sequence number of the source account, allowing it to invalidate any transactions with a smaller sequence number.

See the [`Bump Sequence` errors](../../../errors/result-codes/operation-specific/bump-sequence.md).

 - ATTRIBUTE - DATA TYPE - DESCRIPTION - bump\_to - string - The new desired value for the source account's sequence number.

 \`\`\`json { "\_links": { "self": { "href": "https://horizon.stellar.org/operations/124922916260433921" }, "transaction": { "href": "https://horizon.stellar.org/transactions/f94c338370839a598753221714de0b0193d4fc56ea369db6efe88f18669cc5a1" }, "effects": { "href": "https://horizon.stellar.org/operations/124922916260433921/effects" }, "succeeds": { "href": "https://horizon.stellar.org/effects?order=desc\u0026cursor=124922916260433921" }, "precedes": { "href": "https://horizon.stellar.org/effects?order=asc\u0026cursor=124922916260433921" } }, "id": "124922916260433921", "paging\_token": "124922916260433921", "transaction\_successful": true, "source\_account": "GAYOLLLUIZE4DZMBB2ZBKGBUBZLIOYU6XFLW37GBP2VZD3ABNXCW4BVA", "type": "bump\_sequence", "type\_i": 11, "created\_at": "2020-04-09T00:14:11Z", "transaction\_hash": "f94c338370839a598753221714de0b0193d4fc56ea369db6efe88f18669cc5a1", "bump\_to": "120192344968520085" } \`\`\`

