---
title: Transaction Failed
order: 10
---

# transaction-failed

import { ExampleResponse } from "components/ExampleResponse"; import { AttributeTable } from "components/AttributeTable";

The `transaction_failed` error returns a [`400` error code](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/400) and occurs when a client submits a transaction that was well-formed but was not included in the ledger due to some other failure.

For example, a transaction may fail if: 1. The source account for transaction cannot pay the minimum fee. 2. The sequence number is incorrect. 3. One of the contained operations has failed, such as a payment operation that overdraws on the paying account.

In almost every case, this error indicates that the transaction submitted in the initial request will never succeed. There is one exception: a transaction that fails with the `tx_bad_seq` result code \(as expressed in the `result_code` field of the error\) may become valid in the future if the sequence number it used was too high.

 \`\`\`json { "type": "https://stellar.org/horizon-errors/transaction\_failed", "title": "Transaction Failed", "status": 400, "detail": "The transaction failed when submitted to the stellar network. The \`extras.result\_codes\` field on this response contains further details. Descriptions of each code can be found at: https://www.stellar.org/developers/guides/concepts/list-of-operations.html", "extras": { "envelope\_xdr": "AAAAAgAAAADdfhHDs4Vaug6p8Oxb1QRjNRdJt3pYKKBVhFHrEgd9QAAAAAoAEi4YAAAAAwAAAAEAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAEAAAAAAAAACwAAAAAAAAAAAAAAAAAAAAESB31AAAAAQFhc/liVXbLk3NtB2BtweFJ064JdDIfrTSrqKMhb1oIRK+0PSyvjzZTkRCJmQY3bHNXYNuepa2TF7aBdibrb1gI=", "result\_codes": { "transaction": "tx\_insufficient\_fee" }, "result\_xdr": "AAAAAAAAAAr////3AAAAAA==" } } \`\`\`

