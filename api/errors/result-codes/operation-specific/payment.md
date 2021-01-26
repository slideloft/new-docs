---
title: Payment Result Codes
order: 20
---

# payment

import { ExampleResponse } from "components/ExampleResponse"; import { AttributeTable } from "components/AttributeTable";

These are result codes that communicate success \(200\) or failure \(400\) specific to the `Payment` operation, which often fails because the receiving account does not trust the issuer of the asset being sent.

Learn more about the [`Payment` operation](../../../../start/list-of-operations.md#payment).

 - RESULT CODE - STELLAR PROTOCOL CODE - DESCRIPTION - OpSuccess - PAYMENT\_SUCCESS - The payment was successfully completed. - OpMalformed - PAYMENT\_MALFORMED - The input to the payment is invalid. - OpUnderfunded - PAYMENT\_UNDERFUNDED - The source account \(sender\) does not have enough lumens to send the payment amount while maintaining its own minimum reserve. - OpSrcNoTrust - PAYMENT\_SRC\_NO\_TRUST - The source account does not have a trustline for the asset it is tring to send. - OpSrcNotAuthorized - PAYMENT\_SRC\_NOT\_AUTHORIZED - The source account is not authorized to send this asset. - OpNoDestination - PAYMENT\_NO\_DESTINATION - The destination account does not exist. - OpNoTrust - PAYMENT\_NO\_TRUST - The destination account does not have a trustline for the asset being sent. - OpNotAuthorized - PAYMENT\_NOT\_AUTHORIZED - The destination account is not authorized to hold this asset. - OpLineFull - PAYMENT\_LINE\_FULL - The destination account \(receiver\) does not have sufficient limits to receive amount and still satisfy its buying liabilities. - OpNoIssuer - PAYMENT\_NO\_ISSUER - The issuer of the asset does not exist.

