---
title: Allow Trust Result Codes
order: 100
---

# Allow Trust

These are result codes that communicate success \(200\) or failure \(400\) specific to the `Allow Trust` operation.

Learn more about the [`Allow Trust` operation](../../../../start/list-of-operations.md#allow-trust).

* OpSuccess `ALLOW_TRUST_SUCCESS`

  Trust trust operation was successful.

* OpMalformed `ALLOW_TRUST_MALFORMED`

  The asset specified in type is invalid. In addition, this error happens when the native asset is specified.

* op\_no\_trustline `ALLOW_TRUST_NO_TRUST_LINE`

  The trustor does not have a trustline with the issuer performing this operation.

* op\_not\_required `ALLOW_TRUST_TRUST_NOT_REQUIRED`

  The source account \(issuer performing this operation\) does not require trust. In other words, it does not have the flag AUTH\_REQUIRED\_FLAG set.

* op\_cant\_revoke `ALLOW_TRUST_CANT_REVOKE`

  The source account is trying to revoke the trustline of the trustor, but it cannot do so.

* op\_self\_not\_allowed `ALLOW_TRUST_SELF_NOT_ALLOWED`

  The source account attempted to allow a trustline for itself, which is not allowed because an account cannot create a trustline with itself.

