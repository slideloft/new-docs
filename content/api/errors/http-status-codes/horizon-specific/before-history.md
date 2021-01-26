---
title: Before History
order: 30
---

# before-history

import { ExampleResponse } from "components/ExampleResponse"; import { AttributeTable } from "components/AttributeTable";

A Horizon server may be configured to only keep a portion of the stellar network’s history stored within its database.

The `before_history` error returns a [`410` error code](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/410) and occurs a client requests a piece of information \(such as a page of transactions or a single operation\) that the server can positively identify as falling outside the range of recorded history.

 \`\`\`json { "type": "https://stellar.org/horizon-errors/before\_history", "title": "Data Requested Is Before Recorded History", "status": 410, "detail": "This horizon instance is configured to only track a portion of the stellar network's latest history. This request is asking for results prior to the recorded history known to this horizon instance." } \`\`\`

