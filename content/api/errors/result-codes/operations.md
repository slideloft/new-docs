---
title: Operation Result Codes
order: 20
---

# operations

import { ExampleResponse } from "components/ExampleResponse"; import { AttributeTable } from "components/AttributeTable";

These are Result Codes that communicate success \(200\) or failure \(400\) at the operation level: no source account, too many subentries, etc.

 - RESULT CODE - STELLAR PROTOCOL CODE - DESCRIPTION - op\_inner - opINNER - The inner object result is valid and the operation was a success. - op\_bad\_auth - opBAD\_AUTH - There are too few valid signatures, or the transaction was submitted to the wrong network. - op\_no\_source\_account - opNO\_ACCOUNT - The source account was not found. - op\_not\_supported - opNOT\_SUPPORTED - The operation is not supported at this time. - op\_too\_many\_subentries - opTOO\_MANY\_SUBENTRIES - max number of subentries already reached - op\_exceeded\_work\_limit - opEXCEEDED\_WORK\_LIMIT - operation did too much work

 \`\`\`json { "type": "https://stellar.org/horizon-errors/transaction\_failed", "title": "Transaction Failed", "status": 400, "detail": "The transaction failed when submitted to the stellar network. The \`extras.result\_codes\` field on this response contains further details. Descriptions of each code can be found at: https://www.stellar.org/developers/learn/concepts/list-of-operations.html", "extras": { "envelope\_xdr": "AAAAANPRjCD1iCti3hovsrrz6aSAjmp263grVr6+mI3SQSkcAAAAZAAPRLgAAAADAAAAAAAAAAAAAAABAAAAAQAAAACuSL9OciKkFztj4d3zuadl20HHObu+7qJenBxHPrMayQAAAAUAAAABAAAAANPRjCD1iCti3hovsrrz6aSAjmp263grVr6+mI3SQSkcAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAtJBKRwAAABA1N0iqDAgqS6+3RIZGoNB9OXrY3wd/nLruXYi+eiTt4jn94fLVLwAw6jJCaK+qxStwO7c4kP6u5k0RPbuYC55CT6zGskAAABAiUGCNCS4pGlfcRmi82kbralzcFlTQAFzLyfUrYGn3RtQ4p/7TUwAqIanVoWGfEqzIJo64ZT+mYtJ72BfI+FiDg==", "result\_codes": { "transaction": "tx\_failed", "operations": \["op\_no\_source\_account"\] }, "result\_xdr": "AAAAAAAAAGT/////AAAAAf////4AAAAA" } } \`\`\`

