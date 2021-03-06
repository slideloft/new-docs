---
title: Account Merge Result Codes
order: 110
---

# Account Merge

These are result codes that communicate success \(200\) or failure \(400\) specific to the `Account Merge` operation.

Learn more about the [`Account Merge` operation](../../../../start/list-of-operations.md#account-merge).

* OpSuccess `ACCOUNT_MERGE_SUCCESS`

  Account succesfully merged.

* OpMalformed `ACCOUNT_MERGE_MALFORMED`

  The operation is malformed because the source account cannot merge with itself. The destination must be a different account.

* op\_no\_account `ACCOUNT_MERGE_NO_ACCOUNT`

  The destination account does not exist.

* op\_immutable\_set `ACCOUNT_MERGE_IMMUTABLE_SET`

  The source account has AUTH\_IMMUTABLE flag set.

* op\_has\_sub\_entries `ACCOUNT_MERGE_HAS_SUB_ENTRIES`

  The source account has trustlines and/or offers.

* op\_seq\_num\_too\_far `ACCOUNT_MERGE_SEQNUM_TOO_FAR`

  Source account sequence number is too high.

* op\_dest\_fullACCOUNT\_MERGE\_DEST\_FULL

  The destination account cannot receive the balance of the source account and still satisfy its lumen buying liabilities.

