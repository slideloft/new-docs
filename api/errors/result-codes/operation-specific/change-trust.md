---
title: Change Trust Result Codes
order: 90
---

# Change Trust

These are result codes that communicate success \(200\) or failure \(400\) specific to the `Change Trust` operation.

Learn more about the [`Change Trust` operation](../../../../start/list-of-operations.md#change-trust)

* OpSuccess `CHANGE_TRUST_SUCCESS`

  Trust was successfully changed

* OpMalformed `CHANGE_TRUST_MALFORMED`

  The input to this operation is invalid.

* OpNoIssuer `CHANGE_TRUST_NO_ISSUER`

  The issuer of the asset cannot be found.

* op\_invalid\_limit `CHANGE_TRUST_INVALID_LIMIT`

  The limit is not sufficient to hold the current balance of the trustline and still satisfy its buying liabilities.

* OpLowReserve `CHANGE_TRUST_LOW_RESERVE`

  This account does not have enough XBN to satisfy the minimum XBN reserve increase caused by adding a subentry and still satisfy its XBN selling liabilities. For every new trustline added to an account, the minimum reserve of XBN that account must hold increases.

* op\_self\_not\_allowed `CHANGE_TRUST_SELF_NOT_ALLOWED`

  The source account attempted to create a trustline for itself, which is not allowed.

