---
title: Retrieve Fee Stats
order: 20
---

# single

import { Endpoint } from "components/Endpoint"; import { ExampleResponse } from "components/ExampleResponse"; import { CodeExample } from "components/CodeExample"; import { AttributeTable } from "components/AttributeTable";

The fee stats endpoint provides information about per-operation fee stats over the last 5 ledgers.

 \| \| \| \| --- \| ---------- \| \| GET \| /fee\_stats \|

 \`\`\`curl curl "https://horizon.stellar.org/fee\_stats" \`\`\` \`\`\`js var StellarSdk = require\("stellar-sdk"\); var server = new StellarSdk.Server\("https://horizon.stellar.org"\); server .feeStats\(\) .then\(function \(resp\) { console.log\(resp\); }\) .catch\(function \(err\) { console.error\(err\); }\); \`\`\`

 \`\`\`json { "last\_ledger": "28444696", "last\_ledger\_base\_fee": "100", "ledger\_capacity\_usage": "0.19", "min\_accepted\_fee": "100", "mode\_accepted\_fee": "100", "p10\_accepted\_fee": "100", "p20\_accepted\_fee": "100", "p30\_accepted\_fee": "100", "p40\_accepted\_fee": "100", "p50\_accepted\_fee": "100", "p60\_accepted\_fee": "100", "p70\_accepted\_fee": "100", "p80\_accepted\_fee": "100", "p90\_accepted\_fee": "100", "p95\_accepted\_fee": "100", "p99\_accepted\_fee": "120", "fee\_charged": { "max": "100", "min": "100", "mode": "100", "p10": "100", "p20": "100", "p30": "100", "p40": "100", "p50": "100", "p60": "100", "p70": "100", "p80": "100", "p90": "100", "p95": "100", "p99": "100" }, "max\_fee": { "max": "16000", "min": "100", "mode": "100", "p10": "100", "p20": "100", "p30": "100", "p40": "100", "p50": "100", "p60": "100", "p70": "100", "p80": "100", "p90": "100", "p95": "100", "p99": "120" } } \`\`\`

