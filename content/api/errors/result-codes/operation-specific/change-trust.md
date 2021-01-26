---
title: Change Trust Result Codes
order: 90
---

# change-trust

import { ExampleResponse } from "components/ExampleResponse"; import { AttributeTable } from "components/AttributeTable";

These are result codes that communicate success \(200\) or failure \(400\) specific to the `Change Trust` operation.

Learn more about the [`Change Trust` operation](../../../../docs/start/list-of-operations.md#change-trust)

 - OpSuccess - CHANGE\_TRUST\_SUCCESS - Trust was successfully changed - OpMalformed - CHANGE\_TRUST\_MALFORMED - The input to this operation is invalid. - OpNoIssuer - CHANGE\_TRUST\_NO\_ISSUER - The issuer of the asset cannot be found. - op\_invalid\_limit - CHANGE\_TRUST\_INVALID\_LIMIT - The limit is not sufficient to hold the current balance of the trustline and still satisfy its buying liabilities. - OpLowReserve - CHANGE\_TRUST\_LOW\_RESERVE - This account does not have enough XLM to satisfy the minimum XLM reserve increase caused by adding a subentry and still satisfy its XLM selling liabilities. For every new trustline added to an account, the minimum reserve of XLM that account must hold increases. - op\_self\_not\_allowed - CHANGE\_TRUST\_SELF\_NOT\_ALLOWED - The source account attempted to create a trustline for itself, which is not allowed.

