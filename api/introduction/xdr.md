---
title: XDR
order: 50
---

# xdr

import { ExampleResponse } from "components/ExampleResponse"; import { AttributeTable } from "components/AttributeTable";

In the Stellar network, transactions are encoded using a standardized protocol called [External Data Representation](https://en.wikipedia.org/wiki/External_Data_Representation) \(XDR\).

In Horizon, you will only encounter XDR when [posting](https://github.com/slideloft/new-docs/tree/046158a008b14dc6d54bdd6f4c48e078c303a05e/content/api/resources/transactions/post.mdx) and [getting](../resources/transactions/single.md) transactions and in the [ledger](../resources/ledgers/index.md) header.

When you post a transaction, a client will encode the transaction as XDR before submitting it to Horizon.

When you request a transaction, Horizon returns some data about the transaction in human-readable JSON. The full canonical data about the transaction is encoded in machine-readable XDR, available in XDR attributes at the end of the response.

You can decode this XDR in the Stellar Laboratory’s [XDR Viewer](https://www.stellar.org/laboratory#xdr-viewer).

 - ATTRIBUTE - TYPE - DESCRIPTION - envelope\_xdr - string - The XDR encoded transaction as stellar-core sees it. - result\_xdr - string - The effects of a transaction encoded in XDR. - result\_meta\_xdr - string - The details about the effects of a transaction encoded in XDR. - fee\_meta\_xdr - string - The fees associated with the transaction encoded in XDR.

 \`\`\`json { // Response truncated to highlight XDR-related attributes "envelope\_xdr": "AAAAAPewD+/6X8o0bx3bp49Wf+mUhG3o+TUrcjcst717DWJVAAAAyAFvzscADTkNAAAAAAAAAAAAAAACAAAAAAAAAAYAAAACWE1BVEsAAAAAAAAAAAAAAAPvNOuztX4IjvV8pztsEc1/ZnTz0G3p5Cx4vcf04+xUAAONfqTGgAAAAAAAAAAABQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABAAAAD2NyeXB0b21hcmluZS5ldQAAAAAAAAAAAAAAAAF7DWJVAAAAQK3vfUCZ8mbjW3ssMd0n1tJTF9Fv6EbuJ6cWKkYXBqG5itqanPbFzIQoZEHbPS8nr2vo4dROvKI0uQzNcfExKwM=", "result\_xdr": "AAAAAAAAAMgAAAAAAAAAAgAAAAAAAAAGAAAAAAAAAAAAAAAFAAAAAAAAAAA=", "result\_meta\_xdr": "AAAAAQAAAAIAAAADAZU3mQAAAAAAAAAA97AP7/pfyjRvHdunj1Z/6ZSEbej5NStyNyy3vXsNYlUAAAAABlxskAFvzscADTkMAAAAAgAAAAAAAAAAAAAAD2NyeXB0b21hcmluZS5ldQABAAAAAAAAAAAAAAAAAAAAAAAAAQGVN5kAAAAAAAAAAPewD+/6X8o0bx3bp49Wf+mUhG3o+TUrcjcst717DWJVAAAAAAZcbJABb87HAA05DQAAAAIAAAAAAAAAAAAAAA9jcnlwdG9tYXJpbmUuZXUAAQAAAAAAAAAAAAAAAAAAAAAAAAIAAAACAAAAAwGVN5gAAAABAAAAAPewD+/6X8o0bx3bp49Wf+mUhG3o+TUrcjcst717DWJVAAAAAlhNQVRLAAAAAAAAAAAAAAAD7zTrs7V+CI71fKc7bBHNf2Z089Bt6eQseL3H9OPsVAAATfBgJfPoAAONfqTGgAAAAAABAAAAAAAAAAAAAAABAZU3mQAAAAEAAAAA97AP7/pfyjRvHdunj1Z/6ZSEbej5NStyNyy3vXsNYlUAAAACWE1BVEsAAAAAAAAAAAAAAAPvNOuztX4IjvV8pztsEc1/ZnTz0G3p5Cx4vcf04+xUAABN8GAl8+gAA41+pMaAAAAAAAEAAAAAAAAAAAAAAAIAAAADAZU3mQAAAAAAAAAA97AP7/pfyjRvHdunj1Z/6ZSEbej5NStyNyy3vXsNYlUAAAAABlxskAFvzscADTkNAAAAAgAAAAAAAAAAAAAAD2NyeXB0b21hcmluZS5ldQABAAAAAAAAAAAAAAAAAAAAAAAAAQGVN5kAAAAAAAAAAPewD+/6X8o0bx3bp49Wf+mUhG3o+TUrcjcst717DWJVAAAAAAZcbJABb87HAA05DQAAAAIAAAAAAAAAAAAAAA9jcnlwdG9tYXJpbmUuZXUAAQAAAAAAAAAAAAAAAAAAAA==", "fee\_meta\_xdr": "AAAAAgAAAAMBlTeXAAAAAAAAAAD3sA/v+l/KNG8d26ePVn/plIRt6Pk1K3I3LLe9ew1iVQAAAAAGXG1YAW/OxwANOQwAAAACAAAAAAAAAAAAAAAPY3J5cHRvbWFyaW5lLmV1AAEAAAAAAAAAAAAAAAAAAAAAAAABAZU3mQAAAAAAAAAA97AP7/pfyjRvHdunj1Z/6ZSEbej5NStyNyy3vXsNYlUAAAAABlxskAFvzscADTkMAAAAAgAAAAAAAAAAAAAAD2NyeXB0b21hcmluZS5ldQABAAAAAAAAAAAAAAAAAAAA" // Response truncated to highlight XDR-related attributes } \`\`\`
