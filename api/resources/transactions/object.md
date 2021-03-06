---
title: The Transaction Object
order: 10
---

# Object

When Horizon returns information about a transaction, it uses the following format:

 

* ATTRIBUTEDATA TYPE

  DESCRIPTION

* idstring

  A unique identifier for this transaction.

* paging\_tokennumber

  A cursor value for use in [pagination](https://developers.stellar.org/api/introduction/pagination/).

* successfulboolean

  Indicates if this transaction was successful or not.

* hashstring

  A hex-encoded SHA-256 hash of this transaction’s [XDR](https://developers.stellar.org/docs/glossary/xdr/)-encoded form.

* ledgernumber

  The sequence number of the ledger that this transaction was included in.

* created\_atISO8601 string

  The date this transaction was created.

* source\_accountstring

  The account that originates the transaction.

* source\_account\_sequencestring

  The source account’s sequence number that this transaction consumed.

* fee\_chargednumber

  The fee \(in [stroops](https://developers.stellar.org/docs/issuing-assets/anatomy-of-an-asset/#lumens-xlm)\) paid by the source account to apply this transaction to the ledger.

* max\_feenumber

  The maximum fee \(in [stroops](https://developers.stellar.org/docs/issuing-assets/anatomy-of-an-asset/#lumens-xlm)\) that the source account was willing to pay.

* operation\_countnumber

  The number of operations contained within this transaction.

* envelope\_xdrstring

  A base64 encoded string of the raw `TransactionEnvelope` XDR struct for this transaction.

* result\_xdrstring

  A base64 encoded string of the raw `TransactionResult` XDR struct for this transaction.

* result\_meta\_xdrstring

  A base64 encoded string of the raw `TransactionMeta` XDR struct for this transaction

* fee\_meta\_xdrstring

  A base64 encoded string of the raw `LedgerEntryChanges` XDR struct produced by taking fees for this transaction.

* memostring

  The optional memo attached to a transaction.

* memo\_typestring

  The type of memo. Potential values include `MEMO_TEXT`, `MEMO_ID`, `MEMO_HASH`, `MEMO_RETURN`.

* signaturesstring

  An array of signatures used to sign this transaction.

* valid\_afterRFC3339 date-time string

  The date after which a transaction is valid.

* valid\_beforeRFC3339 date-time string

  The date before which a transaction is valid.

```bash
{
  "memo": "298424",
  "_links": {
    "self": {
      "href": "https://expansion-testnet.bantu.network/transactions/132c440e984ab97d895f3477015080aafd6c4375f6a70a87327f7f95e13c4e31"
    },
    "account": {
      "href": "https://expansion-testnet.bantu.network/accounts/GCO2IP3MJNUOKS4PUDI4C7LGGMQDJGXG3COYX3WSB4HHNAHKYV5YL3VC"
    },
    "ledger": {
      "href": "https://expansion-testnet.bantu.network/ledgers/27956256"
    },
    "operations": {
      "href": "https://expansion-testnet.bantu.network/transactions/132c440e984ab97d895f3477015080aafd6c4375f6a70a87327f7f95e13c4e31/operations{?cursor,limit,order}",
      "templated": true
    },
    "effects": {
      "href": "https://expansion-testnet.bantu.network/transactions/132c440e984ab97d895f3477015080aafd6c4375f6a70a87327f7f95e13c4e31/effects{?cursor,limit,order}",
      "templated": true
    },
    "precedes": {
      "href": "https://expansion-testnet.bantu.network/transactions?order=asc\u0026cursor=120071205238677504"
    },
    "succeeds": {
      "href": "https://expansion-testnet.bantu.network/transactions?order=desc\u0026cursor=120071205238677504"
    }
  },
  "id": "132c440e984ab97d895f3477015080aafd6c4375f6a70a87327f7f95e13c4e31",
  "paging_token": "120071205238677504",
  "successful": true,
  "hash": "132c440e984ab97d895f3477015080aafd6c4375f6a70a87327f7f95e13c4e31",
  "ledger": 27956256,
  "created_at": "2020-01-27T22:13:17Z",
  "source_account": "GCO2IP3MJNUOKS4PUDI4C7LGGMQDJGXG3COYX3WSB4HHNAHKYV5YL3VC",
  "source_account_sequence": "64034663849209932",
  "fee_charged": 100,
  "max_fee": 100,
  "operation_count": 1,
  "envelope_xdr": "AAAAAJ2kP2xLaOVLj6DRwX1mMyA0mubYnYvu0g8OdoDqxXuFAAAAZADjfzAACzBMAAAAAQAAAAAAAAAAAAAAAF4vYIYAAAABAAAABjI5ODQyNAAAAAAAAQAAAAAAAAABAAAAAKdeYELovtcnTxqPEVsdbxHLMoMRalZsK7lo/+3ARzUZAAAAAAAAAADUFJPYAAAAAAAAAAHqxXuFAAAAQBpLpQyh+mwDd5nDSxTaAh5wopBBUaSD1eOK9MdiO+4kWKVTqSr/Ko3kYE/+J42Opsewf81TwINONPbY2CtPggE=",
  "result_xdr": "AAAAAAAAAGQAAAAAAAAAAQAAAAAAAAABAAAAAAAAAAA=",
  "result_meta_xdr": "AAAAAQAAAAIAAAADAaqUIAAAAAAAAAAAnaQ/bEto5UuPoNHBfWYzIDSa5tidi+7SDw52gOrFe4UAAkRg8uGCXADjfzAACzBLAAAAAAAAAAEAAAAAnaQ/bEto5UuPoNHBfWYzIDSa5tidi+7SDw52gOrFe4UAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAAAAAABAaqUIAAAAAAAAAAAnaQ/bEto5UuPoNHBfWYzIDSa5tidi+7SDw52gOrFe4UAAkRg8uGCXADjfzAACzBMAAAAAAAAAAEAAAAAnaQ/bEto5UuPoNHBfWYzIDSa5tidi+7SDw52gOrFe4UAAAAAAAAAAAEAAAAAAAAAAAAAAAAAAAAAAAABAAAABAAAAAMBqoicAAAAAAAAAACnXmBC6L7XJ08ajxFbHW8RyzKDEWpWbCu5aP/twEc1GQAAAAAAmwWMAaVkEgAAAC0AAAAAAAAAAAAAAAAAAAAAAQAAAAAAAAAAAAAAAAAAAAAAAAEBqpQgAAAAAAAAAACnXmBC6L7XJ08ajxFbHW8RyzKDEWpWbCu5aP/twEc1GQAAAADUr5lkAaVkEgAAAC0AAAAAAAAAAAAAAAAAAAAAAQAAAAAAAAAAAAAAAAAAAAAAAAMBqpQgAAAAAAAAAACdpD9sS2jlS4+g0cF9ZjMgNJrm2J2L7tIPDnaA6sV7hQACRGDy4YJcAON/MAALMEwAAAAAAAAAAQAAAACdpD9sS2jlS4+g0cF9ZjMgNJrm2J2L7tIPDnaA6sV7hQAAAAAAAAAAAQAAAAAAAAAAAAAAAAAAAAAAAAEBqpQgAAAAAAAAAACdpD9sS2jlS4+g0cF9ZjMgNJrm2J2L7tIPDnaA6sV7hQACRGAezO6EAON/MAALMEwAAAAAAAAAAQAAAACdpD9sS2jlS4+g0cF9ZjMgNJrm2J2L7tIPDnaA6sV7hQAAAAAAAAAAAQAAAAAAAAAAAAAAAAAAAA==",
  "fee_meta_xdr": "AAAAAgAAAAMBqpQYAAAAAAAAAACdpD9sS2jlS4+g0cF9ZjMgNJrm2J2L7tIPDnaA6sV7hQACRGDy4YLAAON/MAALMEsAAAAAAAAAAQAAAACdpD9sS2jlS4+g0cF9ZjMgNJrm2J2L7tIPDnaA6sV7hQAAAAAAAAAAAQAAAAAAAAAAAAAAAAAAAAAAAAEBqpQgAAAAAAAAAACdpD9sS2jlS4+g0cF9ZjMgNJrm2J2L7tIPDnaA6sV7hQACRGDy4YJcAON/MAALMEsAAAAAAAAAAQAAAACdpD9sS2jlS4+g0cF9ZjMgNJrm2J2L7tIPDnaA6sV7hQAAAAAAAAAAAQAAAAAAAAAAAAAAAAAAAA==",
  "memo_type": "text",
  "signatures": [
    "GkulDKH6bAN3mcNLFNoCHnCikEFRpIPV44r0x2I77iRYpVOpKv8qjeRgT/4njY6mx7B/zVPAg0409tjYK0+CAQ=="
  ],
  "valid_after": "1970-01-01T00:00:00Z",
  "valid_before": "2020-01-27T22:13:26Z"
}
```

