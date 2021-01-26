---
title: Set Options Result Codes
order: 80
---

# set-options

import { ExampleResponse } from "components/ExampleResponse"; import { AttributeTable } from "components/AttributeTable";

These are result codes that communicate success \(200\) or failure \(400\) specific to the `Set Options` operation.

Learn more about the [`Set Options` operation](../../../../docs/start/list-of-operations.md#set-options).

 - OpSuccess - SET\_OPTIONS\_SUCCESS - Options successfully set. - OpLowReserve - SET\_OPTIONS\_LOW\_RESERVE - This account does not have enough XLM to satisfy the minimum XLM reserve increase caused by adding a subentry and still satisfy its XLM selling liabilities. For every new signer added to an account, the minimum reserve of XLM that account must hold increases. - op\_too\_many\_signers - SET\_OPTIONS\_TOO\_MANY\_SIGNERS - 20 is the maximum number of signers an account can have, and adding another signer would exceed that. - op\_bad\_flags - SET\_OPTIONS\_BAD\_FLAGS - The flags set and/or cleared are invalid by themselves or in combination. - op\_invalid\_inflation - SET\_OPTIONS\_INVALID\_INFLATION - The destination account set in the inflation field does not exist. - op\_cant\_change - SET\_OPTIONS\_CANT\_CHANGE - This account can no longer change the option it wants to change. - op\_unknown\_flag - SET\_OPTIONS\_UNKNOWN\_FLAG - The account is trying to set a flag that is unknown. - op\_threshold\_out\_of\_range - SET\_OPTIONS\_THRESHOLD\_OUT\_OF\_RANGE - The value for a key weight or threshold is invalid. - op\_bad\_signer - SET\_OPTIONS\_BAD\_SIGNER - Any additional signers added to the account cannot be the master key. - op\_invalid\_home\_domain - SET\_OPTIONS\_INVALID\_HOME\_DOMAIN - Home domain is malformed.

