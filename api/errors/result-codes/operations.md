---
title: Operation Result Codes
order: 20
---

# Operations

These are Result Codes that communicate success \(200\) or failure \(400\) at the operation level: no source account, too many subentries, etc.

 - RESULT CODE - 

* tx\_success `txSUCCESS`

  The transaction succeeded.

* tx\_failed `txFAILED`

  One of the operations failed \(none were applied\).

* tx\_too\_early `txTOO_EARLY`

  The ledger closeTime was before the minTime.

* tx\_too\_late `txTOO_LATE`

  The ledger closeTime was after the maxTime.

* tx\_missing\_operation `txMISSING_OPERATION`

  No operation was specified

* tx\_bad\_seq `txBAD_SEQ`

  sequence number does not match source account

* tx\_bad\_auth `txBAD_AUTH`

  too few valid signatures / wrong network

* tx\_insufficient\_balance `txINSUFFICIENT_BALANCE`

  fee would bring account below reserve

* tx\_no\_source\_account `txNO_ACCOUNT`

  source account not found

* tx\_insufficient\_fee `txINSUFFICIENT_FEE`

  fee is too small

* tx\_bad\_auth\_extra `txBAD_AUTH_EXTRA`

  unused signatures attached to transaction

* tx\_internal\_error `txINTERNAL_ERROR`

  an unknown error occurred

```bash
{
  "type": "https://expansion-testnet.bantu.network/horizon-errors/transaction_failed",
  "title": "Transaction Failed",
  "status": 400,
  "detail": "The transaction failed when submitted to the stellar network. The `extras.result_codes` field on this response contains further details.  Descriptions of each code can be found at: https://www.stellar.org/developers/learn/concepts/list-of-operations.html",
  "extras": {
    "envelope_xdr": "AAAAANPRjCD1iCti3hovsrrz6aSAjmp263grVr6+mI3SQSkcAAAAZAAPRLgAAAAAAAAAAAAAAAAAAAABAAAAAAAAAAEAAAAArki/TnIipBc7Y+Hd87mnZdtBxzm7vu6iXpwcRz6zGskAAAAAAAAAAAAHoSAAAAAAAAAAAdJBKRwAAABANWeKuRYFmBm1lrMQqMvhbSouwL270SnxcTtv1XI4Y+uVe4yw4Jq7/43EoxwLbRh/pC3V4WfOZRzDqwsTyEztAA==",
    "result_codes": {
      "transaction": "tx_bad_seq"
    },
    "result_xdr": "AAAAAAAAAAD////7AAAAAA=="
  }
}

```

