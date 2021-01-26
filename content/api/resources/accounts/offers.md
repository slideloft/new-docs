---
title: Retrieve an Account's Offers
order: 70
---

# offers

import { Endpoint } from "components/Endpoint"; import { ExampleResponse } from "components/ExampleResponse"; import { CodeExample } from "components/CodeExample"; import { AttributeTable } from "components/AttributeTable";

This endpoint represents all offers a given account has currently open and can be used in streaming mode.

Streaming mode allows you to listen for new offers for this account as they are added to the Stellar ledger. If called in streaming mode, Horizon will start at the earliest known offer unless a `cursor` is set, in which case it will start from that `cursor`. By setting the `cursor` value to `now`, you can stream offers created since your request time.

 \| \| \| \| --- \| --- \| \| GET \| /accounts/:account\_id/offers?cursor={paging\_token}&order={asc,desc}&limit={1-200} \|

 - ARGUMENT - REQUIRED - DESCRIPTION - account\_id - required - This account's public key encoded in a base32 string representation. - cursor - optional - A number that points to a specific location in a collection of responses and is pulled from the \`paging\_token\` value of a record. - order - optional - A designation of the order in which records should appear. Options include \`asc\`\(ascending\) or \`desc\` \(descending\). If this argument isn’t set, it defaults to \`asc\`. - limit - optional - The total number of records returned. The limit can range from 1 to 200 - an upper limit that is hardcoded in Horizon for performance reasons. If this argument isn’t designated, it defaults to 10.

 \`\`\`curl curl "https://horizon.stellar.org/accounts/GD3CJYUTZAY6JQF4CEI6Z7VW5O6VNGKZTBYUECTOJPEDTB7I2HZSPI2K/offers" \`\`\` \`\`\`js var StellarSdk = require\("stellar-sdk"\); var server = new StellarSdk.Server\("https://horizon.stellar.org"\); server .offers\(\) .forAccount\("GD3CJYUTZAY6JQF4CEI6Z7VW5O6VNGKZTBYUECTOJPEDTB7I2HZSPI2K"\) .call\(\) .then\(function \(resp\) { console.log\(resp\); }\) .catch\(function \(err\) { console.error\(err\); }\); \`\`\`

 \`\`\`json { "\_links": { "self": { "href": "https://horizon.stellar.org/accounts/GD3CJYUTZAY6JQF4CEI6Z7VW5O6VNGKZTBYUECTOJPEDTB7I2HZSPI2K/offers?cursor=\u0026limit=10\u0026order=asc" }, "next": { "href": "https://horizon.stellar.org/accounts/GD3CJYUTZAY6JQF4CEI6Z7VW5O6VNGKZTBYUECTOJPEDTB7I2HZSPI2K/offers?cursor=164943216\u0026limit=10\u0026order=asc" }, "prev": { "href": "https://horizon.stellar.org/accounts/GD3CJYUTZAY6JQF4CEI6Z7VW5O6VNGKZTBYUECTOJPEDTB7I2HZSPI2K/offers?cursor=164555927\u0026limit=10\u0026order=desc" } }, "\_embedded": { "records": \[ { "\_links": { "self": { "href": "https://horizon.stellar.org/offers/164555927" }, "offer\_maker": { "href": "https://horizon.stellar.org/accounts/GD3CJYUTZAY6JQF4CEI6Z7VW5O6VNGKZTBYUECTOJPEDTB7I2HZSPI2K" } }, "id": 164555927, "paging\_token": "164555927", "seller": "GD3CJYUTZAY6JQF4CEI6Z7VW5O6VNGKZTBYUECTOJPEDTB7I2HZSPI2K", "selling": { "asset\_type": "native" }, "buying": { "asset\_type": "credit\_alphanum4", "asset\_code": "BB1", "asset\_issuer": "GD5J6HLF5666X4AZLTFTXLY46J5SW7EXRKBLEYPJP33S33MXZGV6CWFN" }, "amount": "214.9999939", "price\_r": { "n": 10000000, "d": 86000001 }, "price": "0.1162791", "last\_modified\_ledger": 28383147, "last\_modified\_time": "2020-02-24T22:58:38Z" }, { "\_links": { "self": { "href": "https://horizon.stellar.org/offers/164943216" }, "offer\_maker": { "href": "https://horizon.stellar.org/accounts/GD3CJYUTZAY6JQF4CEI6Z7VW5O6VNGKZTBYUECTOJPEDTB7I2HZSPI2K" } }, "id": 164943216, "paging\_token": "164943216", "seller": "GD3CJYUTZAY6JQF4CEI6Z7VW5O6VNGKZTBYUECTOJPEDTB7I2HZSPI2K", "selling": { "asset\_type": "credit\_alphanum4", "asset\_code": "BB1", "asset\_issuer": "GD5J6HLF5666X4AZLTFTXLY46J5SW7EXRKBLEYPJP33S33MXZGV6CWFN" }, "buying": { "asset\_type": "native" }, "amount": "24.9999990", "price\_r": { "n": 32224991, "d": 2500000 }, "price": "12.8899964", "last\_modified\_ledger": 28394149, "last\_modified\_time": "2020-02-25T15:49:57Z" } \] } } \`\`\`

 \`\`\`js var StellarSdk = require\("stellar-sdk"\); var server = new StellarSdk.Server\("https://horizon.stellar.org"\); var callback = function \(resp\) { console.log\(resp\); }; var es = server .offers\(\) .forAccount\("GD3CJYUTZAY6JQF4CEI6Z7VW5O6VNGKZTBYUECTOJPEDTB7I2HZSPI2K"\) .cursor\("now"\) .stream\({ onmessage: callback }\); \`\`\`

