---
title: Set Options Object
order: 80
---

# set-options

import { ExampleResponse } from "components/ExampleResponse"; import { AttributeTable } from "components/AttributeTable";

Sets an account's flags, inflation destination, signers, and home domain.

See the [`Set Options` errors](../../../errors/result-codes/operation-specific/set-options.md).

 - ATTRIBUTE - DATA TYPE - DESCRIPTION - signer\_key - string - The public key of the new signer. - signer\_weight - number - The weight of the new signer. Can range from \`1\` to \`255\`. - master\_key\_weight - number - The weight of the master key. Can range from \`1\` to \`255\`. - low\_threshold - number - The sum weight for the low threshold. - med\_threshold - number - The sum weight for the medium threshold. - high\_threshold - number - The sum weight for the high threshold. - home\_domain - string - The home domain used for stellar.toml file discovery. - set\_flags - array - The array of numeric values of flags that has been set in this operation. Options include \`1\` for \`AUTH\_REQUIRED\_FLAG\`, \`2\` for \`AUTH\_REVOCABLE\_FLAG\`, and \`4\` for \`AUTH\_IMMUTABLE\_FLAG\`. - set\_flags\_s - array - The array of string values of flags that has been set in this operation. Options include \`AUTH\_REQUIRED\_FLAG\`, \`AUTH\_REVOCABLE\_FLAG\`, and \`AUTH\_IMMUTABLE\_FLAG\`. - clear\_flags - array - The array of numeric values of flags that has been cleared in this operation. Options include \`1\` for \`AUTH\_REQUIRED\_FLAG\`, \`2\` for \`AUTH\_REVOCABLE\_FLAG\`, and \`4\` for \`AUTH\_IMMUTABLE\_FLAG\`. - clear\_flags\_s - array - The array of string values of flags that has been cleared in this operation. Options include \`AUTH\_REQUIRED\_FLAG\`, \`AUTH\_REVOCABLE\_FLAG\`, and \`AUTH\_IMMUTABLE\_FLAG\`.

 \`\`\`json { "\_links": { "self": { "href": "https://horizon.stellar.org/operations/102125410241826819" }, "transaction": { "href": "https://horizon.stellar.org/transactions/e020277cf755a1c29234d34f123f546a2c4805d7b4ca9303e253667b0ff4d846" }, "effects": { "href": "https://horizon.stellar.org/operations/102125410241826819/effects" }, "succeeds": { "href": "https://horizon.stellar.org/effects?order=desc\u0026cursor=102125410241826819" }, "precedes": { "href": "https://horizon.stellar.org/effects?order=asc\u0026cursor=102125410241826819" } }, "id": "102125410241826819", "paging\_token": "102125410241826819", "transaction\_successful": true, "source\_account": "GABMKJM6I25XI4K7U6XWMULOUQIQ27BCTMLS6BYYSOWKTBUXVRJSXHYQ", "type": "set\_options", "type\_i": 5, "created\_at": "2019-05-08T21:20:34Z", "transaction\_hash": "e020277cf755a1c29234d34f123f546a2c4805d7b4ca9303e253667b0ff4d846", "home\_domain": "www.stellar.org" } \`\`\`

