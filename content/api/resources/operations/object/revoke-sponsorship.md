---
title: Revoke Sponsorship
order: 190
---

# revoke-sponsorship

import { ExampleResponse } from "components/ExampleResponse"; import { AttributeTable } from "components/AttributeTable";

Revoke sponsorship of a ledger entry.

 - ATTRIBUTE - DATA TYPE - DESCRIPTION - account\_id - string \(optional\) - The id of the account which is no longer sponsored. - claimable\_balance\_id - string \(optional\) - The id of the claimable balance which is no longer sponsored. - data\_account\_id - string \(optional\) - The id of the account whose data entry is no longer sponsored. - data\_name - string \(optional\) - The name of the data entry which is no longer sponsored. - offer\_id - string \(optional\) - The id of the offer which is no longer sponsored. - trustline\_account\_id - string \(optional\) - The id of the account whose trustline is no longer sponsored. - trustline\_asset - string \(optional\) - The asset of the trustline which is no longer sponsored. - signer\_account\_id - string \(optional\) - The account id of the signer which is no longer sponsored. - signer\_key - string \(optional\) - The type of the signer which is no longer sponsored.

 \`\`\`json { "\_links": { "self": { "href": "https://horizon.stellar.org/operations/124922916260433921" }, "transaction": { "href": "https://horizon.stellar.org/transactions/f94c338370839a598753221714de0b0193d4fc56ea369db6efe88f18669cc5a1" }, "effects": { "href": "https://horizon.stellar.org/operations/124922916260433921/effects" }, "succeeds": { "href": "https://horizon.stellar.org/effects?order=desc\u0026cursor=124922916260433921" }, "precedes": { "href": "https://horizon.stellar.org/effects?order=asc\u0026cursor=124922916260433921" } }, "id": "124922916260433921", "paging\_token": "124922916260433921", "transaction\_successful": true, "source\_account": "GAYOLLLUIZE4DZMBB2ZBKGBUBZLIOYU6XFLW37GBP2VZD3ABNXCW4BVA", "type": "revoke\_sponsorship", "type\_i": 19, "created\_at": "2020-04-09T00:14:11Z", "transaction\_hash": "f94c338370839a598753221714de0b0193d4fc56ea369db6efe88f18669cc5a1", "account\_id": "GAYOLLLUIZE4DZMBB2ZBKGBUBZLIOYU6XFLW37GBP2VZD3ABNXCW4BVA" } \`\`\`

