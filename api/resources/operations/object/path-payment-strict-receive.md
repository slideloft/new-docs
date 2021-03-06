---
title: Path Payment Strict Receive Object
order: 30
---

# Path Payment Strict Receive

Sends a payment from one account to another in a path through the order books, starting as one asset and ending as another. Path payments that are `Strict Receive` designate the payment amount in the asset received.

See the [`Path Payment Strict Receive` errors](../../../errors/result-codes/operation-specific/path-payment-strict-receive.md).

ATTRIBUTE

* asset\_type `string`

  The type of asset being sent. Either `native`, `credit_alphanum4`, or `credit_alphanum12`.

* asset\_code `string`

  The code for the asset being sent. Appears if the `asset_type` is not `native`.

* asset\_issuer `string`

  The Stellar address of the issuer of the asset being sent. Appears if the `asset_type` is not `native`.

* from `string`

  The payment sender’s public key.

* to `string`

  The payment recipient’s public key.

* amount `string`

  Amount received designated in the source asset.

* patharray of objects

  The intermediary assets that this path hops through.Show child attributes

  * asset\_code `string`

    The code for this intermediary asset.

  * asset\_issuer `string`

    The Stellar address of the intermediary asset’s issuer.

  * asset\_type `string`

    The type for the intermediary asset. Either `native`, `credit_alphanum4`, or `credit_alphanum12`.

* source\_amount `string`

  Amount sent designated in the source asset.

* destination\_min `string`

  The minimum amount of destination asset expected to be received.

* source\_asset\_type `string`

  The type for the source asset. Either `native`, `credit_alphanum4`, or `credit_alphanum12`.

* source\_asset\_code `string`

  The code for the source asset. Appears if the `asset_type` is not `native`.

* source\_asset\_issuer `string`

  The Stellar address of the source asset’s issuer. Appears if the `asset_type` is not `native`.

```bash
{
  "_links": {
    "self": {
      "href": "https://expansion-testnet.bantu.network/operations/124624072438579201"
    },
    "transaction": {
      "href": "https://expansion-testnet.bantu.network/transactions/2b863994825fe85b80bfdff433b348d5ce80b23cd9ee2a56dcd6ee1abd52c9f8"
    },
    "effects": {
      "href": "https://expansion-testnet.bantu.network/operations/124624072438579201/effects"
    },
    "succeeds": {
      "href": "https://expansion-testnet.bantu.network/effects?order=desc\u0026cursor=124624072438579201"
    },
    "precedes": {
      "href": "https://expansion-testnet.bantu.network/effects?order=asc\u0026cursor=124624072438579201"
    }
  },
  "id": "124624072438579201",
  "paging_token": "124624072438579201",
  "transaction_successful": true,
  "source_account": "GBZH7S5NC57XNHKHJ75C5DGMI3SP6ZFJLIKW74K6OSMA5E5DFMYBDD2Z",
  "type": "path_payment_strict_send",
  "type_i": 13,
  "created_at": "2020-04-04T13:47:50Z",
  "transaction_hash": "2b863994825fe85b80bfdff433b348d5ce80b23cd9ee2a56dcd6ee1abd52c9f8",
  "asset_type": "credit_alphanum4",
  "asset_code": "BRL",
  "asset_issuer": "GDVKY2GU2DRXWTBEYJJWSFXIGBZV6AZNBVVSUHEPZI54LIS6BA7DVVSP",
  "from": "GBZH7S5NC57XNHKHJ75C5DGMI3SP6ZFJLIKW74K6OSMA5E5DFMYBDD2Z",
  "to": "GBZH7S5NC57XNHKHJ75C5DGMI3SP6ZFJLIKW74K6OSMA5E5DFMYBDD2Z",
  "amount": "26.5544244",
  "path": [
    {
      "asset_type": "credit_alphanum4",
      "asset_code": "EURT",
      "asset_issuer": "GAP5LETOV6YIE62YAM56STDANPRDO7ZFDBGSNHJQIYGGKSMOZAHOOS2S"
    },
    {
      "asset_type": "native"
    }
  ],
  "source_amount": "5.0000000",
  "destination_min": "26.5544244",
  "source_asset_type": "credit_alphanum4",
  "source_asset_code": "USD",
  "source_asset_issuer": "GDUKMGUGDZQK6YHYA5Z6AY2G4XDSZPSZ3SW5UN3ARVMO6QSRDWP5YLEX"
}
```

