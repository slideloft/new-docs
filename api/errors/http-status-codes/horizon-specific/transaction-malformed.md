---
title: Transaction Malformed
order: 20
---

# transaction-malformed

import { ExampleResponse } from "components/ExampleResponse"; import { AttributeTable } from "components/AttributeTable";

The `transaction_malformed` error returns a [`400` error code](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/400) and occurs when a client submits a malformed transaction.

There are many ways in which a transaction could be malformed, including: 1. You submitted an empty string. 2. Your base64-encoded string is invalid. 3. Your [XDR](../../../introduction/xdr.md) structure is invalid. 4. You have leftover bytes in your [XDR](../../../introduction/xdr.md) structure.

 \`\`\`json { "type": "https://stellar.org/horizon-errors/transaction\_malformed", "title": "Transaction Malformed", "status": 400, "detail": "Horizon could not decode the transaction envelope in this request. A transaction should be an XDR TransactionEnvelope struct encoded using base64. The envelope read from this request is echoed in the \`extras.envelope\_xdr\` field of this response for your convenience.", "extras": { "envelope\_xdr": "BBBBBPORy3CoX6ox2ilbeiVjBA5WlpCSZRcjZ7VE9Wf4QVk7AAAAZAAAQz0AAAACAAAAAAAAAAAAAAABAAAAAAAAAAEAAAAA85HLcKhfqjHaKVt6JWMEDlaWkJJlFyNntUT1Z/hBWTsAAAAAAAAAAAL68IAAAAAAAAAAARN17BEAAABAA9Ad7OKc7y60NT/JuobaHOfmuq8KbZqcV6G/es94u9yT84fi0aI7tJsFMOyy8cZ4meY3Nn908OU+KfRWV40UCw==" } } \`\`\`

