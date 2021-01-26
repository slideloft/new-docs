---
title: Path Payment Strict Send Object
order: 40
---

# path-payment-strict-send

import { ExampleResponse } from "components/ExampleResponse"; import { AttributeTable } from "components/AttributeTable";

Sends a payment from one account to another in a path through the order books, starting as one asset and ending as another. Path payments that are `Strict Send` designate the payment amount in the asset sent.

See the [`Path Payment Strict Send` errors](../../../errors/result-codes/operation-specific/path-payment-strict-send.md).

 - ATTRIBUTE - DATA TYPE - DESCRIPTION - asset\_type - string - The type of asset being sent. Either \`native\`, \`credit\_alphanum4\`, or \`credit\_alphanum12\`. - asset\_code - string - The code for the asset being sent. Appears if the \`asset\_type\` is not \`native\`. - asset\_issuer - string - The Stellar address of the issuer of the asset being sent. Appears if the \`asset\_type\` is not \`native\`. - from - string - The payment sender’s public key. - to - string - The payment recipient’s public key. - amount - string - Amount received designated in the source asset. - path - array of objects - The intermediary assets that this path hops through. - asset\_code - string - The code for this intermediary asset. - asset\_issuer - string - The Stellar address of the intermediary asset’s issuer. - asset\_type - string - The type for the intermediary asset. Either \`native\`, \`credit\_alphanum4\`, or \`credit\_alphanum12\`. - source\_amount - string - Amount sent designated in the source asset. - destination\_min - string - The minimum amount of destination asset expected to be received. - source\_asset\_type - string - The type for the source asset. Either \`native\`, \`credit\_alphanum4\`, or \`credit\_alphanum12\`. - source\_asset\_code - string - The code for the source asset. Appears if the \`asset\_type\` is not \`native\`. - source\_asset\_issuer - string - The Stellar address of the source asset’s issuer. Appears if the \`asset\_type\` is not \`native\`.

 \`\`\`json { "\_links": { "self": { "href": "https://horizon.stellar.org/operations/124624072438579201" }, "transaction": { "href": "https://horizon.stellar.org/transactions/2b863994825fe85b80bfdff433b348d5ce80b23cd9ee2a56dcd6ee1abd52c9f8" }, "effects": { "href": "https://horizon.stellar.org/operations/124624072438579201/effects" }, "succeeds": { "href": "https://horizon.stellar.org/effects?order=desc\u0026cursor=124624072438579201" }, "precedes": { "href": "https://horizon.stellar.org/effects?order=asc\u0026cursor=124624072438579201" } }, "id": "124624072438579201", "paging\_token": "124624072438579201", "transaction\_successful": true, "source\_account": "GBZH7S5NC57XNHKHJ75C5DGMI3SP6ZFJLIKW74K6OSMA5E5DFMYBDD2Z", "type": "path\_payment\_strict\_send", "type\_i": 13, "created\_at": "2020-04-04T13:47:50Z", "transaction\_hash": "2b863994825fe85b80bfdff433b348d5ce80b23cd9ee2a56dcd6ee1abd52c9f8", "asset\_type": "credit\_alphanum4", "asset\_code": "BRL", "asset\_issuer": "GDVKY2GU2DRXWTBEYJJWSFXIGBZV6AZNBVVSUHEPZI54LIS6BA7DVVSP", "from": "GBZH7S5NC57XNHKHJ75C5DGMI3SP6ZFJLIKW74K6OSMA5E5DFMYBDD2Z", "to": "GBZH7S5NC57XNHKHJ75C5DGMI3SP6ZFJLIKW74K6OSMA5E5DFMYBDD2Z", "amount": "26.5544244", "path": \[ { "asset\_type": "credit\_alphanum4", "asset\_code": "EURT", "asset\_issuer": "GAP5LETOV6YIE62YAM56STDANPRDO7ZFDBGSNHJQIYGGKSMOZAHOOS2S" }, { "asset\_type": "native" } \], "source\_amount": "5.0000000", "destination\_min": "26.5544244", "source\_asset\_type": "credit\_alphanum4", "source\_asset\_code": "USD", "source\_asset\_issuer": "GDUKMGUGDZQK6YHYA5Z6AY2G4XDSZPSZ3SW5UN3ARVMO6QSRDWP5YLEX" } \`\`\`
