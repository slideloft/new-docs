---
title: Path Payment Strict Send Object
order: 40
---

# Path Payment Strict Send

Sends a payment from one account to another in a path through the order books, starting as one asset and ending as another. Path payments that are `Strict Send` designate the payment amount in the asset sent.

See the [`Path Payment Strict Send` errors](../../../errors/result-codes/operation-specific/path-payment-strict-send.md).

 ATTRIBUTE

* asset\_type `string`

  The type of asset being received. Either `native`, `credit_alphanum4`, or `credit_alphanum12`.

* asset\_code `string`

  The code for the asset being received. Appears if the `asset_type` is not `native`.

* asset\_issuer `string`

  The Stellar address of the issuer of the asset being received. Appears if the `asset_type` is not `native`.

* from `string`

  The payment sender’s public key.

* tostring

  The payment recipient’s public key.

* amount `string`

  Amount received designated in the destination asset.

* patharray of objects

  The intermediary assets that this path hops through.Show child attributes

  * asset\_code `string`

    The code for this intermediary asset.

  * asset\_issuer `string`

    The Stellar address of the intermediary asset’s issuer.

  * `asset_type string`

    The type for the intermediary asset. Either `native`, `credit_alphanum4`, or `credit_alphanum12`.

* source\_amount `string`

  Amount sent designated in the source asset.

* source\_max `string`

  The maximum amount to be sent designated in the source asset.

* source\_asset\_type `string`

  The type for the source asset. Either `native`, `credit_alphanum4`, or `credit_alphanum12`.

* source\_asset\_code `string`

  The code for the source asset.

* source\_asset\_issuer `string`

  The Stellar address of the source asset’s issuer.

```bash
{
  "_links": {
    "self": {
      "href": "https://horizon.stellar.org/operations/124018825644490753"
    },
    "transaction": {
      "href": "https://horizon.stellar.org/transactions/2624935eefedc195562623d982e501ba2a183382959fa0b9d03cf66dced3b332"
    },
    "effects": {
      "href": "https://horizon.stellar.org/operations/124018825644490753/effects"
    },
    "succeeds": {
      "href": "https://horizon.stellar.org/effects?order=desc\u0026cursor=124018825644490753"
    },
    "precedes": {
      "href": "https://horizon.stellar.org/effects?order=asc\u0026cursor=124018825644490753"
    }
  },
  "id": "124018825644490753",
  "paging_token": "124018825644490753",
  "transaction_successful": true,
  "source_account": "GBZH7S5NC57XNHKHJ75C5DGMI3SP6ZFJLIKW74K6OSMA5E5DFMYBDD2Z",
  "type": "path_payment_strict_receive",
  "type_i": 2,
  "created_at": "2020-03-26T19:33:55Z",
  "transaction_hash": "2624935eefedc195562623d982e501ba2a183382959fa0b9d03cf66dced3b332",
  "asset_type": "credit_alphanum4",
  "asset_code": "BRL",
  "asset_issuer": "GDVKY2GU2DRXWTBEYJJWSFXIGBZV6AZNBVVSUHEPZI54LIS6BA7DVVSP",
  "from": "GBZH7S5NC57XNHKHJ75C5DGMI3SP6ZFJLIKW74K6OSMA5E5DFMYBDD2Z",
  "to": "GBZH7S5NC57XNHKHJ75C5DGMI3SP6ZFJLIKW74K6OSMA5E5DFMYBDD2Z",
  "amount": "0.1000000",
  "path": [
    {
      "asset_type": "credit_alphanum4",
      "asset_code": "USD",
      "asset_issuer": "GBUYUAI75XXWDZEKLY66CFYKQPET5JR4EENXZBUZ3YXZ7DS56Z4OKOFU"
    },
    {
      "asset_type": "native"
    }
  ],
  "source_amount": "0.0198773",
  "source_max": "0.0198774",
  "source_asset_type": "credit_alphanum4",
  "source_asset_code": "USD",
  "source_asset_issuer": "GDUKMGUGDZQK6YHYA5Z6AY2G4XDSZPSZ3SW5UN3ARVMO6QSRDWP5YLEX"
}
```

