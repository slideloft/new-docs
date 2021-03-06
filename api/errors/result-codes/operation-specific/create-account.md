---
title: Create Account Result Codes
order: 10
---

# Create Account

These are result codes that communicate success \(200\) or failure \(400\) specific to the `Create Account` operation, which often fails because the new account does not meet the minimum reserve.

Learn more about the [`Create Account` operation](../../../../start/list-of-operations.md#create-account).

 - RESULT CODE -

* OpSuccess `CREATE_ACCOUNT_SUCCESS`

  The inner object result is valid, the operation was a success, and an acount was created.

* OpMalformed `CREATE_ACCOUNT_MALFORMED`

  The destination was invalid.

* OpUnderfunded `CREATE_ACCOUNT_UNDERFUNDED`

  The source account performing the command does not have enough funds to give the destination account the necessary mininum reserve and still maintain its own minimum reserve.

* OpLowReserve `CREATE_ACCOUNT_LOW_RESERVE`

  The operation would create an account below the minimum reserve.

* OpAlreadyExists `CREATE_ACCOUNT_ALREADY_EXIST`

  The destination account already exists.



