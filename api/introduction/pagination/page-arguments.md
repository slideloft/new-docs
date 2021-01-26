---
title: Page Arguments
order: 10
---

# page-arguments

import { Endpoint } from "components/Endpoint"; import { ExampleResponse } from "components/ExampleResponse"; import { AttributeTable } from "components/AttributeTable"; import { CodeExample } from "components/CodeExample";

 \| \| \| \| --- \| ---------------------------------------------------------------- \| \| GET \| /{endpoint}?cursor={paging\_token}&order={asc,desc}&limit={1-200} \|

 - ARGUMENT - REQUIRED? - DESCRIPTION - cursor - optional - A number that points to a specific location in a collection of responses and is pulled from the \`paging\_token\` value of a record. - order - optional - A designation of the order in which records should appear. Options include \`asc\`\(ascending\) or \`desc\` \(descending\). If this argument isn’t set, it defaults to \`asc\`. - limit - optional - The total number of records returned. The limit can range from 1 to 200 - an upper limit that is hardcoded in Horizon for performance reasons. If this argument isn’t designated, it defaults to 10.

 \`\`\`curl curl "https://horizon.stellar.org/ledgers/26478723/operations?cursor=113725249324879872&limit=5&order=asc" \`\`\` \`\`\`js var StellarSdk = require\("stellar-sdk"\); var server = new StellarSdk.Server\("https://horizon.stellar.org"\); server .operations\(\) .forLedger\("26478723"\) .cursor\("113725249324879872"\) .limit\(5\) .order\("asc"\) .call\(\) .then\(function \(resp\) { console.log\(resp\); }\) .catch\(function \(err\) { console.error\(err\); }\); \`\`\`

 \`\`\`json { "\_links": { "self": { "href": "https://horizon.stellar.org/ledgers/26478723/operations?cursor=113725249324879872\u0026limit=5\u0026order=asc" }, "next": { "href": "https://horizon.stellar.org/ledgers/26478723/operations?cursor=113725249324916737\u0026limit=5\u0026order=asc" }, "prev": { "href": "https://horizon.stellar.org/ledgers/26478723/operations?cursor=113725249324879873\u0026limit=5\u0026order=desc" } }, "\_embedded": { "records": \[ { "\_links": { "self": { "href": "https://horizon.stellar.org/operations/113725249324879873" }, "transaction": { "href": "https://horizon.stellar.org/transactions/6adab48bbc0a38b9d40938b63a8ae0f5b334948c2d5acfb755dea616f98720d1" }, "effects": { "href": "https://horizon.stellar.org/operations/113725249324879873/effects" }, "succeeds": { "href": "https://horizon.stellar.org/effects?order=desc\u0026cursor=113725249324879873" }, "precedes": { "href": "https://horizon.stellar.org/effects?order=asc\u0026cursor=113725249324879873" } }, "id": "113725249324879873", "paging\_token": "113725249324879873", "transaction\_successful": true, "source\_account": "GCRGHKY6RBFVQLF2JCHB7TK7A5BIABITFKVIEOXK4BPEIDE446OEFYXZ", "type": "manage\_offer", "type\_i": 3, "created\_at": "2019-10-25T20:45:51Z", "transaction\_hash": "6adab48bbc0a38b9d40938b63a8ae0f5b334948c2d5acfb755dea616f98720d1", "amount": "5048.0792092", "price": "0.0000079", "price\_r": { "n": 79, "d": 10000000 }, "buying\_asset\_type": "credit\_alphanum4", "buying\_asset\_code": "BTC", "buying\_asset\_issuer": "GATEMHCCKCY67ZUCKTROYN24ZYT5GK4EQZ65JJLDHKHRUZI3EUEKMTCH", "selling\_asset\_type": "native", "offer\_id": 125121197 }, { "\_links": { "self": { "href": "https://horizon.stellar.org/operations/113725249324888065" }, "transaction": { "href": "https://horizon.stellar.org/transactions/c4de60af4815d94b6f3aa9947403f96dd0e8c3ba7d84eccce9c2c798470381ed" }, "effects": { "href": "https://horizon.stellar.org/operations/113725249324888065/effects" }, "succeeds": { "href": "https://horizon.stellar.org/effects?order=desc\u0026cursor=113725249324888065" }, "precedes": { "href": "https://horizon.stellar.org/effects?order=asc\u0026cursor=113725249324888065" } }, "id": "113725249324888065", "paging\_token": "113725249324888065", "transaction\_successful": true, "source\_account": "GCFKS7EBBZQTBBM7HHOASGZBE3L2TADWG6OJBVJXYIS44LQFXFL766UB", "type": "manage\_offer", "type\_i": 3, "created\_at": "2019-10-25T20:45:51Z", "transaction\_hash": "c4de60af4815d94b6f3aa9947403f96dd0e8c3ba7d84eccce9c2c798470381ed", "amount": "103.0721239", "price": "0.0655000", "price\_r": { "n": 131, "d": 2000 }, "buying\_asset\_type": "credit\_alphanum4", "buying\_asset\_code": "USD", "buying\_asset\_issuer": "GDSRCV5VTM3U7Y3L6DFRP3PEGBNQMGOWSRTGSBWX6Z3H6C7JHRI4XFJP", "selling\_asset\_type": "native", "offer\_id": 0 }, { "\_links": { "self": { "href": "https://horizon.stellar.org/operations/113725249324892161" }, "transaction": { "href": "https://horizon.stellar.org/transactions/6d0fe444dd346e05742776305f5e90dd102bd83dfa00a54cfd79bd94753beba0" }, "effects": { "href": "https://horizon.stellar.org/operations/113725249324892161/effects" }, "succeeds": { "href": "https://horizon.stellar.org/effects?order=desc\u0026cursor=113725249324892161" }, "precedes": { "href": "https://horizon.stellar.org/effects?order=asc\u0026cursor=113725249324892161" } }, "id": "113725249324892161", "paging\_token": "113725249324892161", "transaction\_successful": true, "source\_account": "GB44WLYD6HQXZHLRCPARIAMBASN35TDHXU5Q3I3DRHQMLLB3CBMIZLY5", "type": "manage\_buy\_offer", "type\_i": 12, "created\_at": "2019-10-25T20:45:51Z", "transaction\_hash": "6d0fe444dd346e05742776305f5e90dd102bd83dfa00a54cfd79bd94753beba0", "amount": "2942.0268642", "price": "6.7000000", "price\_r": { "n": 67, "d": 10 }, "buying\_asset\_type": "credit\_alphanum4", "buying\_asset\_code": "SLT", "buying\_asset\_issuer": "GCKA6K5PCQ6PNF5RQBF7PQDJWRHO6UOGFMRLK3DYHDOI244V47XKQ4GP", "selling\_asset\_type": "native", "offer\_id": 0 }, { "\_links": { "self": { "href": "https://horizon.stellar.org/operations/113725249324908545" }, "transaction": { "href": "https://horizon.stellar.org/transactions/36907ac7f802a079fa1d7e7fddeb31decbed1218b47924243daaa508af8b1bbe" }, "effects": { "href": "https://horizon.stellar.org/operations/113725249324908545/effects" }, "succeeds": { "href": "https://horizon.stellar.org/effects?order=desc\u0026cursor=113725249324908545" }, "precedes": { "href": "https://horizon.stellar.org/effects?order=asc\u0026cursor=113725249324908545" } }, "id": "113725249324908545", "paging\_token": "113725249324908545", "transaction\_successful": true, "source\_account": "GBVI7F7QBE3ZEHP7HUAXAEKENITQKCXR5CML5JMOCHJN6EOQXLTSJYJI", "type": "payment", "type\_i": 1, "created\_at": "2019-10-25T20:45:51Z", "transaction\_hash": "36907ac7f802a079fa1d7e7fddeb31decbed1218b47924243daaa508af8b1bbe", "asset\_type": "credit\_alphanum4", "asset\_code": "TFC", "asset\_issuer": "GDS3XDJAA4VY6MJYASIGSIMPHZ7AQNZ54RKLWT7MWCOU5YKYEVCNLVS3", "from": "GBVI7F7QBE3ZEHP7HUAXAEKENITQKCXR5CML5JMOCHJN6EOQXLTSJYJI", "to": "GAMKXMT23OMMOFJMZIHT5T3C65JI5YGAOHJMDYBBS4JJBB3X2CVLT3GO", "amount": "0.0380000" }, { "\_links": { "self": { "href": "https://horizon.stellar.org/operations/113725249324916737" }, "transaction": { "href": "https://horizon.stellar.org/transactions/785058d3363b448c95943a40230333b8d523607c9617089bb17c9202a2e7384a" }, "effects": { "href": "https://horizon.stellar.org/operations/113725249324916737/effects" }, "succeeds": { "href": "https://horizon.stellar.org/effects?order=desc\u0026cursor=113725249324916737" }, "precedes": { "href": "https://horizon.stellar.org/effects?order=asc\u0026cursor=113725249324916737" } }, "id": "113725249324916737", "paging\_token": "113725249324916737", "transaction\_successful": true, "source\_account": "GDD7ABRF7BCK76W33RXDQG5Q3WXVSQYVLGEMXSOWRGZ6Z3G3M2EM2TCP", "type": "manage\_offer", "type\_i": 3, "created\_at": "2019-10-25T20:45:51Z", "transaction\_hash": "785058d3363b448c95943a40230333b8d523607c9617089bb17c9202a2e7384a", "amount": "0.0000000", "price": "1.0000000", "price\_r": { "n": 1, "d": 1 }, "buying\_asset\_type": "native", "selling\_asset\_type": "credit\_alphanum4", "selling\_asset\_code": "BTC", "selling\_asset\_issuer": "GBVOL67TMUQBGL4TZYNMY3ZQ5WGQYFPFD5VJRWXR72VA33VFNL225PL5", "offer\_id": 125126043 } \] } } \`\`\`
