---
title: Path Payment Strict Send Result Codes
order: 40
---

# path-payment-strict-send

import { ExampleResponse } from "components/ExampleResponse"; import { AttributeTable } from "components/AttributeTable";

These are result codes that communicate success \(200\) or failure \(400\) specific to the `Path Payment Strict Send` operation.

Learn more about the [`Path Payment Strict Send` operation](../../../../docs/start/list-of-operations.md#path-payment-strict-send).

 - RESULT CODE - STELLAR PROTOCOL CODE - DESCRIPTION - OpSuccess - PATH\_PAYMENT\_STRICT\_SEND\_SUCCESS - The payment was successfully completed. - OpMalformed - PATH\_PAYMENT\_STRICT\_SEND\_MALFORMED - The input for this path payment is invalid. - OpUnderfunded - PATH\_PAYMENT\_STRICT\_SEND\_UNDERFUNDED - The source account \(sender\) does not have enough lumens to send the payment amount while maintaining its own minimum reserve. - OpSrcNoTrust - PATH\_PAYMENT\_STRICT\_SEND\_SRC\_NO\_TRUST - The source account is missing the appropriate trustline. - OpSrcNotAuthorized - PATH\_PAYMENT\_STRICT\_SEND\_SRC\_NOT\_AUTHORIZED - The source account is not authorized to send this asset. - OpNoDestination - PATH\_PAYMENT\_STRICT\_SEND\_NO\_DESTINATION - The destination account does not exist. - OpNoTrust - PATH\_PAYMENT\_STRICT\_SEND\_NO\_TRUST - The destination account does not have a trustline for the asset being sent. - OpNotAuthorized - PATH\_PAYMENT\_STRICT\_SEND\_NOT\_AUTHORIZED - The destination account is not authorized to hold this asset. - OpLineFull - PATH\_PAYMENT\_STRICT\_SEND\_LINE\_FULL - The destination account \(receiver\) does not have sufficient limits to receive amount and still satisfy its buying liabilities. - OpNoIssuer - PATH\_PAYMENT\_STRICT\_SEND\_NO\_ISSUER - The issuer of one of the assets is missing. - OpTooFewOffers - PATH\_PAYMENT\_STRICT\_SEND\_TOO\_FEW\_OFFERS - There is no path of offers connecting the send asset and destination asset. Stellar only considers paths of length 5 or shorter. - OpCrossSelf - PATH\_PAYMENT\_STRICT\_SEND\_OFFER\_CROSS\_SELF - This path payment would cross one of its own offers. - OpUnderDestMin - PATH\_PAYMENT\_STRICT\_SEND\_UNDER\_DESTMIN - The paths that could send destination amount of destination asset would fall short of destination min.

