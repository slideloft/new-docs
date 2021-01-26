---
title: Create Account Result Codes
order: 10
---

# create-account

import { ExampleResponse } from "components/ExampleResponse"; import { AttributeTable } from "components/AttributeTable";

These are result codes that communicate success \(200\) or failure \(400\) specific to the `Create Account` operation, which often fails because the new account does not meet the minimum reserve.

Learn more about the [`Create Account` operation](../../../../start/list-of-operations.md#create-account).

 - RESULT CODE - STELLAR PROTOCOL CODE - DESCRIPTION - OpSuccess - CREATE\_ACCOUNT\_SUCCESS - The inner object result is valid, the operation was a success, and an acount was created. - OpMalformed - CREATE\_ACCOUNT\_MALFORMED - The destination was invalid. - OpUnderfunded - CREATE\_ACCOUNT\_UNDERFUNDED - The source account performing the command does not have enough funds to give the destination account the necessary mininum reserve and still maintain its own minimum reserve. - OpLowReserve - CREATE\_ACCOUNT\_LOW\_RESERVE - The operation would create an account below the minimum reserve. - OpAlreadyExists - CREATE\_ACCOUNT\_ALREADY\_EXIST - The destination account already exists.

