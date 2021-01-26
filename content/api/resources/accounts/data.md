---
title: Retrieve an Account's Data
order: 90
---

# data

import { Endpoint } from "components/Endpoint"; import { ExampleResponse } from "components/ExampleResponse"; import { CodeExample } from "components/CodeExample"; import { AttributeTable } from "components/AttributeTable";

This endpoint represents a single data for a given account.

 \| \| \| \| --- \| ------------------------------- \| \| GET \| /accounts/:account\_id/data/:key \|

 - ARGUMENT - REQUIRED - DESCRIPTION - account\_id - required - This account's public key encoded in a base32 string representation. - key - required - The key name for this data.

 \`\`\`curl curl "https://horizon.stellar.org/accounts/GCAXBKU3AKYJPLQ6PEJ6L47KOATCYCBJ2NFRGAK7FUUA2DCEUC265SU2/data/config.memo\_required" \`\`\` \`\`\`js var StellarSdk = require\("stellar-sdk"\); var server = new StellarSdk.Server\("https://horizon.stellar.org"\); server .loadAccount\("GCAXBKU3AKYJPLQ6PEJ6L47KOATCYCBJ2NFRGAK7FUUA2DCEUC265SU2"\) .then\(function \(account\) { return account.data\({ key: "config.memo\_required" }\); }\) .then\(function \(resp\) { console.log\(resp\); }\) .catch\(function \(err\) { console.error\(err\); }\); \`\`\`

 \`\`\`json { "value": "MQ==" } \`\`\`

