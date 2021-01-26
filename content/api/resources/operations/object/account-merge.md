---
title: Account Merge Object
order: 110
---

# account-merge

import { ExampleResponse } from "components/ExampleResponse"; import { AttributeTable } from "components/AttributeTable";

Removes the source account from the Stellar and transfers the source account's lumens to another account.

See the [`Account Merge` errors](../../../errors/result-codes/operation-specific/account-merge.md).

 - ATTRIBUTE - DATA TYPE - DESCRIPTION - account - string - The Stellar address being removed. - into - string - The Stellar address receiving the deleted account's lumens.

 \`\`\`json { "\_links": { "self": { "href": "https://horizon.stellar.org/operations/121887714411839489" }, "transaction": { "href": "https://horizon.stellar.org/transactions/02077009a551ec94c776f83529293dcfc1c2cd5b38af043ef7f3699bf5a71f0a" }, "effects": { "href": "https://horizon.stellar.org/operations/121887714411839489/effects" }, "succeeds": { "href": "https://horizon.stellar.org/effects?order=desc\u0026cursor=121887714411839489" }, "precedes": { "href": "https://horizon.stellar.org/effects?order=asc\u0026cursor=121887714411839489" } }, "id": "121887714411839489", "paging\_token": "121887714411839489", "transaction\_successful": true, "source\_account": "GCVLWV5B3L3YE6DSCCMHLCK7QIB365NYOLQLW3ZKHI5XINNMRLJ6YHVX", "type": "account\_merge", "type\_i": 8, "created\_at": "2020-02-24T17:03:00Z", "transaction\_hash": "02077009a551ec94c776f83529293dcfc1c2cd5b38af043ef7f3699bf5a71f0a", "account": "GCVLWV5B3L3YE6DSCCMHLCK7QIB365NYOLQLW3ZKHI5XINNMRLJ6YHVX", "into": "GATL3ETTZ3XDGFXX2ELPIKCZL7S5D2HY3VK4T7LRPD6DW5JOLAEZSZBA" } \`\`\`

