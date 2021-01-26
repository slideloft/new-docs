---
title: Manage Data Result Codes
order: 120
---

# manage-data

import { ExampleResponse } from "components/ExampleResponse"; import { AttributeTable } from "components/AttributeTable";

These are result codes that communicate success \(200\) or failure \(400\) specific to the `Manage Data` operation.

Learn more about the [`Manage Data` operation](../../../../start/list-of-operations.md#manage-data).

 - OpSuccess - MANAGE\_DATA\_SUCCESS - Manage data operation has executed successfully. - op\_not\_supported\_yet - MANAGE\_DATA\_NOT\_SUPPORTED\_YET - The network hasn’t moved to this protocol change yet. This failure means the network doesn’t support this feature yet. - op\_data\_name\_not\_found - MANAGE\_DATA\_NAME\_NOT\_FOUND - Trying to remove a Data Entry that isn’t there. This will happen if Name is set \(and Value isn’t\) but the Account doesn’t have a DataEntry with that Name. - op\_low\_reserve - MANAGE\_DATA\_LOW\_RESERVE - This account does not have enough XLM to satisfy the minimum XLM reserve increase caused by adding a subentry and still satisfy its XLM selling liabilities. For every new DataEntry added to an account, the minimum reserve of XLM that account must hold increases. - op\_data\_invalid\_name - MANAGE\_DATA\_INVALID\_NAME - Name not a valid string.

