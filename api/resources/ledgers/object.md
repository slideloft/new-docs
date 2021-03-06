---
title: The Ledger Object
order: 10
---

# Object



When Horizon returns information about a ledger, it uses the following format:

* ATTRIBUTEDATA TYPE

  DESCRIPTION

* idstring

  A unique identifier for this ledger.

* paging\_tokennumber

  A cursor value for use in [pagination](https://developers.stellar.org/api/introduction/pagination/).

* hashstring

  A hex-encoded SHA-256 hash of this ledger’s [XDR](https://developers.stellar.org/docs/glossary/xdr/)-encoded form.

* prev\_hashstring

  The hash of the ledger immediately preceding this ledger.

* sequencenumber

  The sequence number of this ledger, and the parameter used in Horizon calls that require a ledger number.

* successful\_transaction\_countnumber

  The number of successful transactions in this ledger.

* failed\_transaction\_countnumber

  The number of failed transactions in this ledger.

* operation\_countnumber

  The number of operations applied in this ledger.

* closed\_atstring

  An [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601) formatted string of when this ledger was closed.

* total\_coinsstring

  The total number of lumens in circulation.

* fee\_poolstring

  The sum of all transaction fees.

* base\_fee\_in\_stroopsnumber

  The fee the network charges per operation in a transaction.

* base\_reserve\_in\_stroopsnumber

  The reserve the network uses when calculating an account’s minimum balance.

* max\_tx\_set\_sizenumber

  The maximum number of transactions validators have agreed to process in a given ledger.

* protocol\_versionnumber

  The protocol version that the Stellar network was running when this ledger was committed.

* header\_xdrstring

  A base64 encoded string of the raw `LedgerHeader` xdr struct for this ledger.

```javascript
{
  "_links": {
    "self": {
      "href": "https://horizon.stellar.org/ledgers/26857634"
    },
    "transactions": {
      "href": "https://horizon.stellar.org/ledgers/26857634/transactions{?cursor,limit,order}",
      "templated": true
    },
    "operations": {
      "href": "https://horizon.stellar.org/ledgers/26857634/operations{?cursor,limit,order}",
      "templated": true
    },
    "payments": {
      "href": "https://horizon.stellar.org/ledgers/26857634/payments{?cursor,limit,order}",
      "templated": true
    },
    "effects": {
      "href": "https://horizon.stellar.org/ledgers/26857634/effects{?cursor,limit,order}",
      "templated": true
    }
  },
  "id": "548393ec23959e1959a62f003029ecf96be89e13df036073bf64918996ec4227",
  "paging_token": "115352659677937664",
  "hash": "548393ec23959e1959a62f003029ecf96be89e13df036073bf64918996ec4227",
  "prev_hash": "446d6eca81dd6db6daf50d93ca9d297bd60b1233b91de3765cccdf503cfffcb0",
  "sequence": 26857634,
  "successful_transaction_count": 27,
  "failed_transaction_count": 1,
  "operation_count": 133,
  "closed_at": "2019-11-18T19:27:21Z",
  "total_coins": "105443902087.3472865",
  "fee_pool": "1807038.9789761",
  "base_fee_in_stroops": 100,
  "base_reserve_in_stroops": 5000000,
  "max_tx_set_size": 1000,
  "protocol_version": 12,
  "header_xdr": "AAAADERtbsqB3W222vUNk8qdKXvWCxIzuR3jdlzM31A8//ywoQieYsSc05/BpgEqnLR7fKXz7t0K42V7NOjbGZA/wTEAAAAAXdLwmQAAAAAAAAAAplf68mTg/Z/DDyEZeLCoNbJnMZm4SYsYWjUjuDOSfPeRNFE4n9Hm19yKutjwVurFjk72JKVHI8J+ELwLZgWsywGZ0KIOoh6z7HlbYQAAEG9XKhRBAAABFgAAAAAH9M6YAAAAZABMS0AAAAPop9+CeMs1/7BHgFltiQPH+VT+ACYb5P0lSXh7RpBLtd34kEpeL8qKJxYz4ufmkQ2lEv/HMR/i3bi1Rt0PYj185/0kAZ3ZRbmm2mVRMzmaCOak1rn2vejHXDh+MGlr6D6vI2tc/M6VIumTKUa7SgumWDyW0r5FcJTbu/FXDQ/6C4YAAAAA"
}
```

