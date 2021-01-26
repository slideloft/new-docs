---
title: Allow Trust Object
order: 100
---

# allow-trust

import { ExampleResponse } from "components/ExampleResponse"; import { AttributeTable } from "components/AttributeTable";

Updates the “authorized” flag of an existing trust line. This must be called by the issuer of the asset.

See the [`Allow Trust` errors](../../../errors/result-codes/operation-specific/allow-trust.md).

 - ATTRIBUTE - DATA TYPE - DESCRIPTION - asset\_type - string - The type of asset. Either \`native\`, \`credit\_alphanum4\`, or \`credit\_alphanum12\`. - asset\_code - string - The Stellar address of the asset. - asset\_issuer - string - The code for the asset. - authorize - int - Flag indicating whether the trustline is authorized. 0 if the account is not authorized to transact with the asset in any way. 1 if the account is authorized to transact with the asset. 2 if the account is authorized to maintain orders, but not to perform other transactions. - trustee - string - The issuing account, or source account in this instance. - trustor - string - The trusting account, or the account being authorized or unauthorized.

 \`\`\`json { "\_links": { "self": { "href": "https://horizon.stellar.org/operations/120497059836067841" }, "transaction": { "href": "https://horizon.stellar.org/transactions/ac8dd0ddf1d047081c8e4c2a7ef9cc38a1a8af6c211184e1b16ebf2e32915d7f" }, "effects": { "href": "https://horizon.stellar.org/operations/120497059836067841/effects" }, "succeeds": { "href": "https://horizon.stellar.org/effects?order=desc\u0026cursor=120497059836067841" }, "precedes": { "href": "https://horizon.stellar.org/effects?order=asc\u0026cursor=120497059836067841" } }, "id": "120497059836067841", "paging\_token": "120497059836067841", "transaction\_successful": true, "source\_account": "GCRZQVBBDAWVOCO5R2NI34YR55RO2GQXPTDUE5OZESXGZRRTAEQLKEKN", "type": "allow\_trust", "type\_i": 7, "created\_at": "2020-02-03T14:30:52Z", "transaction\_hash": "ac8dd0ddf1d047081c8e4c2a7ef9cc38a1a8af6c211184e1b16ebf2e32915d7f", "asset\_type": "credit\_alphanum4", "asset\_code": "LSV1", "asset\_issuer": "GCRZQVBBDAWVOCO5R2NI34YR55RO2GQXPTDUE5OZESXGZRRTAEQLKEKN", "trustee": "GCRZQVBBDAWVOCO5R2NI34YR55RO2GQXPTDUE5OZESXGZRRTAEQLKEKN", "trustor": "GDSYBYRG6NIBJWR7BLY72HYV7VM4A7WWHUJ45FI7H4Q2U2RPR3BB3CFR", "authorize": true } \`\`\`

