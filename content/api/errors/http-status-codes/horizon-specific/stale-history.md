---
title: Stale History
order: 40
---

# stale-history

import { ExampleResponse } from "components/ExampleResponse"; import { AttributeTable } from "components/AttributeTable";

A Horizon server may be configured to reject historical requests when the history is known to be further out of date than the configured threshold.

In such cases, the `stale_history` error occurs and returns a [`503` error code](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/503). To resolve this error \(provided you are the Horizon instance’s operator\), please ensure that the ingestion system is running correctly and importing new ledgers.

 \`\`\`json { "type": "https://stellar.org/horizon-errors/stale\_history", "title": "Historical DB Is Too Stale", "status": 503, "detail": "This horizon instance is configured to reject client requests when it can determine that the history database is lagging too far behind the connected instance of stellar-core. If you operate this server, please ensure that the ingestion system is properly running." } \`\`\`

