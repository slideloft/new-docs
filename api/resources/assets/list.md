---
title: List All Assets
order: 20
---

# list

import { Endpoint } from "components/Endpoint"; import { ExampleResponse } from "components/ExampleResponse"; import { CodeExample } from "components/CodeExample"; import { AttributeTable } from "components/AttributeTable";

This endpoint lists all assets.

 \| \| \| \| --- \| --- \| \| GET \| /assets?asset\_code{:asset\_code}&asset\_issuer={:account\_id}&cursor={paging\_token}&order={asc,desc}&limit={1-200}&include\_failed{true,false} \|

 - ARGUMENT - REQUIRED - DESCRIPTION - asset\_code - optional - The code of the asset you would like to filter by. - asset\_issuer - optional - The Stellar address of the issuer for the asset you would like to filter by. - cursor - optional - A number that points to a specific location in a collection of responses and is pulled from the \`paging\_token\` value of a record. - order - optional - A designation of the order in which records should appear. Options include \`asc\`\(ascending\) or \`desc\` \(descending\). If this argument isn’t set, it defaults to \`asc\`. - limit - optional - The total number of records returned. The limit can range from 1 to 200 - an upper limit that is hardcoded in Horizon for performance reasons. If this argument isn’t designated, it defaults to 10.

 \`\`\`curl curl "https://horizon.stellar.org/assets?asset\_code=CNY&limit=3" \`\`\` \`\`\`js var StellarSdk = require\("stellar-sdk"\); var server = new StellarSdk.Server\("https://horizon.stellar.org"\); server .assets\(\) .forCode\("CNY"\) .call\(\) .then\(function \(resp\) { console.log\(resp\); }\) .catch\(function \(err\) { console.error\(err\); }\); \`\`\`

 \`\`\`json { "\_links": { "self": { "href": "https://horizon.stellar.org/assets?asset\_code=CNY\u0026cursor=\u0026limit=3\u0026order=asc" }, "next": { "href": "https://horizon.stellar.org/assets?asset\_code=CNY\u0026cursor=CNY\_GATEMHCCKCY67ZUCKTROYN24ZYT5GK4EQZ65JJLDHKHRUZI3EUEKMTCH\_credit\_alphanum4\u0026limit=3\u0026order=asc" }, "prev": { "href": "https://horizon.stellar.org/assets?asset\_code=CNY\u0026cursor=CNY\_GAOT23KBW2HL6HVZFPNFLLT5VGIKGTLGR3AFDHYSRIWS4QKBYRPUW4N3\_credit\_alphanum4\u0026limit=3\u0026order=desc" } }, "\_embedded": { "records": \[ { "\_links": { "toml": { "href": "https://stellar.chenyuzhifu.com/.well-known/stellar.toml" } }, "asset\_type": "credit\_alphanum4", "asset\_code": "CNY", "asset\_issuer": "GAOT23KBW2HL6HVZFPNFLLT5VGIKGTLGR3AFDHYSRIWS4QKBYRPUW4N3", "paging\_token": "CNY\_GAOT23KBW2HL6HVZFPNFLLT5VGIKGTLGR3AFDHYSRIWS4QKBYRPUW4N3\_credit\_alphanum4", "amount": "997268.0000000", "num\_accounts": 23, "flags": { "auth\_required": false, "auth\_revocable": false, "auth\_immutable": false } }, { "\_links": { "toml": { "href": "https://ripplefox.com/.well-known/stellar.toml" } }, "asset\_type": "credit\_alphanum4", "asset\_code": "CNY", "asset\_issuer": "GAREELUB43IRHWEASCFBLKHURCGMHE5IF6XSE7EXDLACYHGRHM43RFOX", "paging\_token": "CNY\_GAREELUB43IRHWEASCFBLKHURCGMHE5IF6XSE7EXDLACYHGRHM43RFOX\_credit\_alphanum4", "amount": "18318343.2623217", "num\_accounts": 5514, "flags": { "auth\_required": false, "auth\_revocable": false, "auth\_immutable": false } }, { "\_links": { "toml": { "href": "https://naobtc.com/.well-known/stellar.toml" } }, "asset\_type": "credit\_alphanum4", "asset\_code": "CNY", "asset\_issuer": "GATEMHCCKCY67ZUCKTROYN24ZYT5GK4EQZ65JJLDHKHRUZI3EUEKMTCH", "paging\_token": "CNY\_GATEMHCCKCY67ZUCKTROYN24ZYT5GK4EQZ65JJLDHKHRUZI3EUEKMTCH\_credit\_alphanum4", "amount": "0.0000000", "num\_accounts": 1, "flags": { "auth\_required": false, "auth\_revocable": false, "auth\_immutable": false } } \] } } \`\`\`

 \`\`\`js var StellarSdk = require\("stellar-sdk"\); var server = new StellarSdk.Server\("https://horizon.stellar.org"\); var callback = function \(resp\) { console.log\(resp\); }; var es = server .assets\(\) .forCode\("CNY"\) .cursor\("now"\) .stream\({ onmessage: callback }\); \`\`\`

