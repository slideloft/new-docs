---
title: Error Response
order: 10
---

# Response

When an error occurs, Horizon responds with a JSON document with the below attributes.

 - ATTRIBUTE - 

* type `URL`

  The type of Status Code returned.

* title `string`

  A short title describing the Status Code, which can be used to lookup more information about an error.

* status `number`

  A short title describing the Status Code, which can be used to lookup more information about an error.

* detail `string`

  A short title describing the Status Code, which can be used to lookup more information about an error.

* extras `array`

  If the Status Code is `Transaction Failed`, this extras field displays the Result Code returned by Stellar Core describing why the transaction failed. Hide child attributes

  * envelope\_xdr `string`

    A base64-encoded representation of the TransactionEnvelope XDR whose failure triggered this response.

  * result\_xdr `string`

    A base64-encoded representation of the TransactionResult XDR returned by stellar-core when submitting this transaction.

  * result\_codes.transaction `string`

    The transaction Result Code returned by Stellar Core, which can be used to lookup more information about an error in the docs.

  * result\_codes.operations `array`

    An array of operation Result Codes returned by Stellar Core, which can be used to lookup more information about an error in the docs.

```bash
{
  "type": "https://expansion-testnet.bantu.network/horizon-errors/transaction_failed",
  "title": "Transaction Failed",
  "status": 400,
  "detail": "The transaction failed when submitted to the stellar network. The `extras.result_codes` field on this response contains further details.  Descriptions of each code can be found at: https://www.stellar.org/developers/learn/concepts/list-of-operations.html",
  "extras": {
    "envelope_xdr": "AAAAANPRjCD1iCti3hovsrrz6aSAjmp263grVr6+mI3SQSkcAAAAZAAPRLgAAAADAAAAAAAAAAAAAAABAAAAAQAAAACuSL9OciKkFztj4d3zuadl20HHObu+7qJenBxHPrMayQAAAAUAAAABAAAAANPRjCD1iCti3hovsrrz6aSAjmp263grVr6+mI3SQSkcAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAtJBKRwAAABA1N0iqDAgqS6+3RIZGoNB9OXrY3wd/nLruXYi+eiTt4jn94fLVLwAw6jJCaK+qxStwO7c4kP6u5k0RPbuYC55CT6zGskAAABAiUGCNCS4pGlfcRmi82kbralzcFlTQAFzLyfUrYGn3RtQ4p/7TUwAqIanVoWGfEqzIJo64ZT+mYtJ72BfI+FiDg==",
    "result_codes": {
      "transaction": "tx_failed",
      "operations": ["op_no_source_account"]
    },
    "result_xdr": "AAAAAAAAAGT/////AAAAAf////4AAAAA"
  }
}
```

