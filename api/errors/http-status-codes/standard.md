---
title: Standard Status Codes
order: 10
---

# standard

import { ExampleResponse } from "components/ExampleResponse"; import { AttributeTable } from "components/AttributeTable";

These responses are Internet protocol codes that describe basic issues with a submitted transaction.

 - STATUS CODE - VALUE - DESCRIPTION - OK - 200 - The request has succeeded. - Bad Request - 400 - The request as invalid in some way. - Not Found - 404 - The requested resource does not exist. - Not Implemented - 404 - The request does not have an acceptable response content-type. - Not Acceptable - 406 - The request does not have an acceptable response content-type. - Internal Server Error - 500 - Something went wrong on the Horizon server’s end.

 \`\`\`json { "type": "https://stellar.org/horizon-errors/bad\_request", "title": "Bad Request", "status": 400, "detail": "The request you sent was invalid in some way", "extras": { "invalid\_field": "limit", "reason": "unparseable value" } } \`\`\`

