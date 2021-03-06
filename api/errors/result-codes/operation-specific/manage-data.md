---
title: Manage Data Result Codes
order: 120
---

# Manage Data

These are result codes that communicate success \(200\) or failure \(400\) specific to the `Manage Data` operation.

Learn more about the [`Manage Data` operation](../../../../start/list-of-operations.md#manage-data). 

* OpSuccess `MANAGE_DATA_SUCCESS`

  Manage data operation has executed successfully.

* op\_not\_supported\_yet `MANAGE_DATA_NOT_SUPPORTED_YET`

  The network hasn’t moved to this protocol change yet. This failure means the network doesn’t support this feature yet.

* op\_data\_name\_not\_found `MANAGE_DATA_NAME_NOT_FOUND`

  Trying to remove a Data Entry that isn’t there. This will happen if Name is set \(and Value isn’t\) but the Account doesn’t have a DataEntry with that Name.

* op\_low\_reserve `MANAGE_DATA_LOW_RESERVE`

  This account does not have enough XBN to satisfy the minimum XBN reserve increase caused by adding a subentry and still satisfy its XBN selling liabilities. For every new DataEntry added to an account, the minimum reserve of XBN that account must hold increases.

* op\_data\_invalid\_name `MANAGE_DATA_INVALID_NAME`

  Name not a valid string.

