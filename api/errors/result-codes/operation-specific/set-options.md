---
title: Set Options Result Codes
order: 80
---

# Set Options

These are result codes that communicate success \(200\) or failure \(400\) specific to the `Set Options` operation.

Learn more about the [`Set Options` operation](../../../../start/list-of-operations.md#set-options).

* OpSuccess `SET_OPTIONS_SUCCESS`

  Options successfully set.

* OpLowReserve `SET_OPTIONS_LOW_RESERVE`

  This account does not have enough XBN to satisfy the minimum XBN reserve increase caused by adding a subentry and still satisfy its XBN selling liabilities. For every new signer added to an account, the minimum reserve of XBN that account must hold increases.

* op\_too\_many\_signers `SET_OPTIONS_TOO_MANY_SIGNERS`

  20 is the maximum number of signers an account can have, and adding another signer would exceed that.

* op\_bad\_flags `SET_OPTIONS_BAD_FLAGS`

  The flags set and/or cleared are invalid by themselves or in combination.

* op\_invalid\_inflation `SET_OPTIONS_INVALID_INFLATION`

  The destination account set in the inflation field does not exist.

* op\_cant\_change `SET_OPTIONS_CANT_CHANGE`

  This account can no longer change the option it wants to change.

* op\_unknown\_flag `SET_OPTIONS_UNKNOWN_FLAG`

  The account is trying to set a flag that is unknown.

* op\_threshold\_out\_of\_rangeSET\_OPTIONS\_THRESHOLD\_OUT\_OF\_RANGE

  The value for a key weight or threshold is invalid.

* op\_bad\_signer `SET_OPTIONS_BAD_SIGNER`

  Any additional signers added to the account cannot be the master key.

* op\_invalid\_home\_domain `SET_OPTIONS_INVALID_HOME_DOMAIN`

  Home domain is malformed.

