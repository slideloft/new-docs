---
title: Error Response
order: 10
---

# response

import { ExampleResponse } from "components/ExampleResponse"; import { AttributeTable } from "components/AttributeTable";

When any error occurs, Horizon responds with a JSON document with the below attributes.

 - ATTRIBUTE - DATA TYPE - DESCRIPTION - type - URL - The type of Status Code returned. - title - string - A short title describing the Status Code, which can be used to look up more information about a error. - status - number - A short title describing the Status Code, which can be used to look up more information about a error. - detail - string - A short title describing the Status Code, which can be used to look up more information about a error. - extras - array - If the Status Code is \`Transaction Failed\`, this extras field displays the Result Code returned by Stellar Core describing why the transaction failed. - envelope\_xdr - string - A base64-encoded representation of the TransactionEnvelope XDR whose failure triggered this response. - result\_xdr - string - A base64-encoded representation of the TransactionResult XDR returned by stellar-core when submitting this transaction. - result\_codes.transaction - string - The transaction Result Code returned by Stellar Core, which can be used to look up more information about an error in the docs. - result\_codes.operations - array - An array of operation Result Codes returned by Stellar Core, which can be used to look up more information about an error in the docs.

 \`\`\`json { "type": "https://stellar.org/horizon-errors/transaction\_failed", "title": "Transaction Failed", "status": 400, "detail": "The transaction failed when submitted to the stellar network. The \`extras.result\_codes\` field on this response contains further details. Descriptions of each code can be found at: https://www.stellar.org/developers/learn/concepts/list-of-operations.html", "extras": { "envelope\_xdr": "AAAAANPRjCD1iCti3hovsrrz6aSAjmp263grVr6+mI3SQSkcAAAAZAAPRLgAAAADAAAAAAAAAAAAAAABAAAAAQAAAACuSL9OciKkFztj4d3zuadl20HHObu+7qJenBxHPrMayQAAAAUAAAABAAAAANPRjCD1iCti3hovsrrz6aSAjmp263grVr6+mI3SQSkcAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAtJBKRwAAABA1N0iqDAgqS6+3RIZGoNB9OXrY3wd/nLruXYi+eiTt4jn94fLVLwAw6jJCaK+qxStwO7c4kP6u5k0RPbuYC55CT6zGskAAABAiUGCNCS4pGlfcRmi82kbralzcFlTQAFzLyfUrYGn3RtQ4p/7TUwAqIanVoWGfEqzIJo64ZT+mYtJ72BfI+FiDg==", "result\_codes": { "transaction": "tx\_failed", "operations": \["op\_no\_source\_account"\] }, "result\_xdr": "AAAAAAAAAGT/////AAAAAf////4AAAAA" } } \`\`\`

