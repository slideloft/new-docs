---
title: The Asset Object
order: 10
---

# object

import { ExampleResponse } from "components/ExampleResponse"; import { AttributeTable } from "components/AttributeTable";

When Horizon returns information about an asset, it uses the following format:

 - ATTRIBUTE - DATA TYPE - DESCRIPTION - asset\_type - string - This asset's type. Either \`credit\_alphanum4\` or \`credit\_alphanum12\`. - asset\_code - string - This asset's code - asset\_issuer - string - The Stellar address of this asset’s issuer. - amount - number - The number of units issued for this asset. - num\_accounts - number - The numnber of accounts that have issued a trustline to this asset. If the \`auth\_required\` flag for this asset's issuer is set to \`true\`, this number only includes the accounts who have both set up a trustline to the asset and have been authorized to hold the asset. - flags - object - Flags denote the enabling/disabling of certain asset issuer privileges. - auth\_immutable - boolean - If set to \`true\`, none of the following flags can be changed. - auth\_required - boolean - If set to \`true\`, anyone who wants to hold an asset issued by this account must first be approved by this account. - auth\_revocable - boolean - If set to \`true\`, this account can freeze the balance of a holder of an asset issued by this account. - paging\_token - number - A cursor value for use in \[pagination\]\(../../introduction/pagination/index.mdx\).

 \`\`\`json { "\_links": { "self": { "href": "https://horizon.stellar.org/assets?asset\_code=USD\u0026asset\_issuer=GDUKMGUGDZQK6YHYA5Z6AY2G4XDSZPSZ3SW5UN3ARVMO6QSRDWP5YLEX\u0026cursor=\u0026limit=10\u0026order=asc" }, "next": { "href": "https://horizon.stellar.org/assets?asset\_code=USD\u0026asset\_issuer=GDUKMGUGDZQK6YHYA5Z6AY2G4XDSZPSZ3SW5UN3ARVMO6QSRDWP5YLEX\u0026cursor=USD\_GDUKMGUGDZQK6YHYA5Z6AY2G4XDSZPSZ3SW5UN3ARVMO6QSRDWP5YLEX\_credit\_alphanum4\u0026limit=10\u0026order=asc" }, "prev": { "href": "https://horizon.stellar.org/assets?asset\_code=USD\u0026asset\_issuer=GDUKMGUGDZQK6YHYA5Z6AY2G4XDSZPSZ3SW5UN3ARVMO6QSRDWP5YLEX\u0026cursor=USD\_GDUKMGUGDZQK6YHYA5Z6AY2G4XDSZPSZ3SW5UN3ARVMO6QSRDWP5YLEX\_credit\_alphanum4\u0026limit=10\u0026order=desc" } }, "\_embedded": { "records": \[ { "\_links": { "toml": { "href": "https://www.anchorusd.com/.well-known/stellar.toml" } }, "asset\_type": "credit\_alphanum4", "asset\_code": "USD", "asset\_issuer": "GDUKMGUGDZQK6YHYA5Z6AY2G4XDSZPSZ3SW5UN3ARVMO6QSRDWP5YLEX", "paging\_token": "USD\_GDUKMGUGDZQK6YHYA5Z6AY2G4XDSZPSZ3SW5UN3ARVMO6QSRDWP5YLEX\_credit\_alphanum4", "amount": "1347404.4083346", "num\_accounts": 9390, "flags": { "auth\_required": false, "auth\_revocable": false, "auth\_immutable": false } } \] } } \`\`\`

