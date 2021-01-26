---
title: Retrieve an Order Book
order: 20
---

# single

import { Endpoint } from "components/Endpoint"; import { ExampleResponse } from "components/ExampleResponse"; import { CodeExample } from "components/CodeExample"; import { AttributeTable } from "components/AttributeTable";

The order book endpoint provides an order book's bids and asks and can be used in [streaming](../../introduction/streaming.md) mode.

When filtering for a specific order book, you must use use all six of these arguments: `base_asset_type`, `base_asset_issuer`, `base_asset_code`, `counter_asset_type`, `counter_asset_issuer`, and `counter_asset_code`. If the base or counter asset is XLM, you only need to indicate the asset type as `native` and do not need to designate the code or the issuer.

 \| \| \| \| --- \| --- \| \| GET \| /order\_book?selling\_asset\_type={native,credit\_alphanum4,credit\_alphanum12}&selling\_asset\_issuer={:account\_id}&selling\_asset\_code{:asset\_code}&buying\_asset\_type={native,credit\_alphanum4,credit\_alphanum12}&buying\_asset\_issuer={:account\_id}&buying\_asset\_code{:asset\_code}&limit={1-200} \|

 - ARGUMENT - REQUIRED - DESCRIPTION - selling\_asset\_type - required - The type for the asset being sold \(base asset\). Either \`native\`, \`credit\_alphanum4\`, or \`credit\_alphanum12\`. - selling\_asset\_issuer - optional - The Stellar address of the issuer of the asset being sold \(base asset\). Required if the \`selling\_asset\_type\` is not \`native\`. - selling\_asset\_code - optional - The code for the asset being sold \(base asset\). Required if the \`selling\_asset\_type\` is not \`native\`. - buying\_asset\_type - required - The type for the asset being bought \(counter asset\). Either \`native\`, \`credit\_alphanum4\`, or \`credit\_alphanum12\`. - buying\_asset\_issuer - optional - The Stellar address of the issuer of the asset being bought \(counter asset\). Required if the \`buying\_asset\_type\` is not \`native\`. - buying\_asset\_code - optional - The code for the asset being bought \(counter asset\). Required if the \`buying\_asset\_type\` is not \`native\`. - limit - optional - The total number of records returned. The limit can range from 1 to 200—an upper limit that is hardcoded in Horizon for performance reasons. If this argument isn’t designated, it defaults to 20 for order books.

 \`\`\`curl curl "https://horizon.stellar.org/order\_book?selling\_asset\_type=native&buying\_asset\_type=credit\_alphanum4&buying\_asset\_code=BB1&buying\_asset\_issuer=GD5J6HLF5666X4AZLTFTXLY46J5SW7EXRKBLEYPJP33S33MXZGV6CWFN&limit=4" \`\`\` \`\`\`js var StellarSdk = require\("stellar-sdk"\); var server = new StellarSdk.Server\("https://horizon.stellar.org"\); server .orderbook\( new StellarSdk.Asset.native\(\), new StellarSdk.Asset\( "BB1", "GD5J6HLF5666X4AZLTFTXLY46J5SW7EXRKBLEYPJP33S33MXZGV6CWFN", \), \) .call\(\) .then\(function \(resp\) { console.log\(resp\); }\) .catch\(function \(err\) { console.error\(err\); }\); \`\`\`

 \`\`\`json { "bids": \[ { "price\_r": { "n": 10000000, "d": 139999999 }, "price": "0.0714286", "amount": "24.9999990" }, { "price\_r": { "n": 1, "d": 14 }, "price": "0.0714286", "amount": "188.0000000" }, { "price\_r": { "n": 1, "d": 15 }, "price": "0.0666667", "amount": "230.3200000" }, { "price\_r": { "n": 1, "d": 16 }, "price": "0.0625000", "amount": "50.0000000" } \], "asks": \[ { "price\_r": { "n": 5000000, "d": 62500001 }, "price": "0.0800000", "amount": "4.9400001" }, { "price\_r": { "n": 10000000, "d": 125000001 }, "price": "0.0800000", "amount": "2516.5154327" }, { "price\_r": { "n": 2, "d": 25 }, "price": "0.0800000", "amount": "3125.0000000" }, { "price\_r": { "n": 4, "d": 49 }, "price": "0.0816327", "amount": "4593.7500000" } \], "base": { "asset\_type": "native" }, "counter": { "asset\_type": "credit\_alphanum4", "asset\_code": "BB1", "asset\_issuer": "GD5J6HLF5666X4AZLTFTXLY46J5SW7EXRKBLEYPJP33S33MXZGV6CWFN" } } \`\`\`

 \`\`\`js var StellarSdk = require\("stellar-sdk"\); var server = new StellarSdk.Server\("https://horizon.stellar.org"\); var callback = function \(resp\) { console.log\(resp\); }; var es = server .orderbook\( new StellarSdk.Asset.native\(\), new StellarSdk.Asset\( "BB1", "GD5J6HLF5666X4AZLTFTXLY46J5SW7EXRKBLEYPJP33S33MXZGV6CWFN", \), \) .cursor\("now"\) .stream\({ onmessage: callback }\); \`\`\`

