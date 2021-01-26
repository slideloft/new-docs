---
title: Payment Object
order: 20
---

# payment

import { ExampleResponse } from "components/ExampleResponse"; import { AttributeTable } from "components/AttributeTable";

Sends an amount in a specific asset to a destination account.

See the [`Payment` errors](../../../errors/result-codes/operation-specific/payment.md).

 - ATTRIBUTE - DATA TYPE - DESCRIPTION - asset\_type - string - The type of asset being sent. Either \`native\`, \`credit\_alphanum4\`, or \`credit\_alphanum12\`. - asset\_code - string - The code for the asset being sent. Appears if the \`asset\_type\` is not \`native\`. - asset\_issuer - string - The Stellar address of the issuer of the asset being sent. Appears if the \`asset\_type\` is not \`native\`. - from - string - The payment sender’s public key. - to - string - The payment recipient’s public key. - amount - string - Amount sent.

 \`\`\`json { "\_links": { "self": { "href": "https://horizon.stellar.org/operations/122511124621283329" }, "transaction": { "href": "https://horizon.stellar.org/transactions/452a180790caf4dbe658d996316cd727ce5573f5f0a77790da540cc49214fe80" }, "effects": { "href": "https://horizon.stellar.org/operations/122511124621283329/effects" }, "succeeds": { "href": "https://horizon.stellar.org/effects?order=desc\u0026cursor=122511124621283329" }, "precedes": { "href": "https://horizon.stellar.org/effects?order=asc\u0026cursor=122511124621283329" } }, "id": "122511124621283329", "paging\_token": "122511124621283329", "transaction\_successful": true, "source\_account": "GCAXBKU3AKYJPLQ6PEJ6L47KOATCYCBJ2NFRGAK7FUUA2DCEUC265SU2", "type": "payment", "type\_i": 1, "created\_at": "2020-03-04T22:46:47Z", "transaction\_hash": "452a180790caf4dbe658d996316cd727ce5573f5f0a77790da540cc49214fe80", "asset\_type": "credit\_alphanum4", "asset\_code": "NGNT", "asset\_issuer": "GAWODAROMJ33V5YDFY3NPYTHVYQG7MJXVJ2ND3AOGIHYRWINES6ACCPD", "from": "GCAXBKU3AKYJPLQ6PEJ6L47KOATCYCBJ2NFRGAK7FUUA2DCEUC265SU2", "to": "GC2QCKFI3DOBEYVBONPVNA2PMLU225IKKI6XPENMWR2CTWSFBAOU7T34", "amount": "5.0000000" } \`\`\`

