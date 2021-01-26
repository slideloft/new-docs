---
title: Account Merge Result Codes
order: 110
---

# account-merge

import { ExampleResponse } from "components/ExampleResponse"; import { AttributeTable } from "components/AttributeTable";

These are result codes that communicate success \(200\) or failure \(400\) specific to the `Account Merge` operation.

Learn more about the [`Account Merge` operation](../../../../start/list-of-operations.md#account-merge).

 - OpSuccess - ACCOUNT\_MERGE\_SUCCESS - Account succesfully merged. - OpMalformed - ACCOUNT\_MERGE\_MALFORMED - The operation is malformed because the source account cannot merge with itself. The destination must be a different account. - op\_no\_account - ACCOUNT\_MERGE\_NO\_ACCOUNT - The destination account does not exist. - op\_immutable\_set - ACCOUNT\_MERGE\_IMMUTABLE\_SET - The source account has AUTH\_IMMUTABLE flag set. - op\_has\_sub\_entries - ACCOUNT\_MERGE\_HAS\_SUB\_ENTRIES - The source account has trustlines and/or offers. - op\_seq\_num\_too\_far - ACCOUNT\_MERGE\_SEQNUM\_TOO\_FAR - Source account sequence number is too high. - op\_dest\_full - ACCOUNT\_MERGE\_DEST\_FULL - The destination account cannot receive the balance of the source account and still satisfy its lumen buying liabilities.

