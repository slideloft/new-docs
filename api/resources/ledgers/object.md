---
title: The Ledger Object
order: 10
---

# object

import { ExampleResponse } from "components/ExampleResponse"; import { AttributeTable } from "components/AttributeTable";

When Horizon returns information about a ledger, it uses the following format:

 - ATTRIBUTE - DATA TYPE - DESCRIPTION - id - string - A unique identifier for this ledger. - paging\_token - number - A cursor value for use in \[pagination\]\(../../introduction/pagination/index.mdx\). - hash - string - A hex-encoded SHA-256 hash of this ledger’s \[XDR\]\(../../../docs/glossary/xdr.mdx\)-encoded form. - prev\_hash - string - The hash of the ledger immediately preceding this ledger. - sequence - number - The sequence number of this ledger, and the parameter used in Horizon calls that require a ledger number. - successful\_transaction\_count - number - The number of successful transactions in this ledger. - failed\_transaction\_count - number - The number of failed transactions in this ledger. - operation\_count - number - The number of operations applied in this ledger. - closed\_at - string - An \[ISO 8601\]\(https://en.wikipedia.org/wiki/ISO\_8601\) formatted string of when this ledger was closed. - total\_coins - string - The total number of lumens in circulation. - fee\_pool - string - The sum of all transaction fees. - base\_fee\_in\_stroops - number - The fee the network charges per operation in a transaction. - base\_reserve\_in\_stroops - number - The reserve the network uses when calculating an account’s minimum balance. - max\_tx\_set\_size - number - The maximum number of transactions validators have agreed to process in a given ledger. - protocol\_version - number - The protocol version that the Stellar network was running when this ledger was committed. - header\_xdr - string - A base64 encoded string of the raw \`LedgerHeader\` xdr struct for this ledger.

 \`\`\`json { "\_links": { "self": { "href": "https://horizon.stellar.org/ledgers/26857634" }, "transactions": { "href": "https://horizon.stellar.org/ledgers/26857634/transactions{?cursor,limit,order}", "templated": true }, "operations": { "href": "https://horizon.stellar.org/ledgers/26857634/operations{?cursor,limit,order}", "templated": true }, "payments": { "href": "https://horizon.stellar.org/ledgers/26857634/payments{?cursor,limit,order}", "templated": true }, "effects": { "href": "https://horizon.stellar.org/ledgers/26857634/effects{?cursor,limit,order}", "templated": true } }, "id": "548393ec23959e1959a62f003029ecf96be89e13df036073bf64918996ec4227", "paging\_token": "115352659677937664", "hash": "548393ec23959e1959a62f003029ecf96be89e13df036073bf64918996ec4227", "prev\_hash": "446d6eca81dd6db6daf50d93ca9d297bd60b1233b91de3765cccdf503cfffcb0", "sequence": 26857634, "successful\_transaction\_count": 27, "failed\_transaction\_count": 1, "operation\_count": 133, "closed\_at": "2019-11-18T19:27:21Z", "total\_coins": "105443902087.3472865", "fee\_pool": "1807038.9789761", "base\_fee\_in\_stroops": 100, "base\_reserve\_in\_stroops": 5000000, "max\_tx\_set\_size": 1000, "protocol\_version": 12, "header\_xdr": "AAAADERtbsqB3W222vUNk8qdKXvWCxIzuR3jdlzM31A8//ywoQieYsSc05/BpgEqnLR7fKXz7t0K42V7NOjbGZA/wTEAAAAAXdLwmQAAAAAAAAAAplf68mTg/Z/DDyEZeLCoNbJnMZm4SYsYWjUjuDOSfPeRNFE4n9Hm19yKutjwVurFjk72JKVHI8J+ELwLZgWsywGZ0KIOoh6z7HlbYQAAEG9XKhRBAAABFgAAAAAH9M6YAAAAZABMS0AAAAPop9+CeMs1/7BHgFltiQPH+VT+ACYb5P0lSXh7RpBLtd34kEpeL8qKJxYz4ufmkQ2lEv/HMR/i3bi1Rt0PYj185/0kAZ3ZRbmm2mVRMzmaCOak1rn2vejHXDh+MGlr6D6vI2tc/M6VIumTKUa7SgumWDyW0r5FcJTbu/FXDQ/6C4YAAAAA" } \`\`\`
