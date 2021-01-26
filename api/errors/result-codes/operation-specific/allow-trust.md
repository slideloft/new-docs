---
title: Allow Trust Result Codes
order: 100
---

# allow-trust

import { ExampleResponse } from "components/ExampleResponse"; import { AttributeTable } from "components/AttributeTable";

These are result codes that communicate success \(200\) or failure \(400\) specific to the `Allow Trust` operation.

Learn more about the [`Allow Trust` operation](../../../../start/list-of-operations.md#allow-trust).

 - OpSuccess - ALLOW\_TRUST\_SUCCESS - Trust trust operation was successful. - OpMalformed - ALLOW\_TRUST\_MALFORMED - The asset specified in type is invalid. In addition, this error happens when the native asset is specified. - op\_no\_trustline - ALLOW\_TRUST\_NO\_TRUST\_LINE - The trustor does not have a trustline with the issuer performing this operation. - op\_not\_required - ALLOW\_TRUST\_TRUST\_NOT\_REQUIRED - The source account \(issuer performing this operation\) does not require trust. In other words, it does not have the flag AUTH\_REQUIRED\_FLAG set. - op\_cant\_revoke - ALLOW\_TRUST\_CANT\_REVOKE - The source account is trying to revoke the trustline of the trustor, but it cannot do so. - op\_self\_not\_allowed - ALLOW\_TRUST\_SELF\_NOT\_ALLOWED - The source account attempted to allow a trustline for itself, which is not allowed because an account cannot create a trustline with itself.

