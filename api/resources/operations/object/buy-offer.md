---
title: Manage Buy Offer Object
order: 60
---

# Buy Offer

Creates, updates, or deletes a buy offer to trade assets. A buy offer specifies a certain amount of the buying asset that should be sold in exchange for the minimum quantity of the selling asset.

See the [`Manage Buy Offer` errors](../../../errors/result-codes/operation-specific/manage-buy-offer.md).

ATTRIBUTE



* amount `string`

  The amount of `buying_asset` that the account making this offer is willing to buy.

* price `string`

  How many units of `buying_asset` it takes to get 1 unit of `selling_asset`. A number representing the decimal form of `price_r`.

* price\_r `object`

  A precise representation of the buy and sell price of the assets on offer.Show child attributes

  * * 

* buying\_asset\_type `string`

  The type for the buying asset. Either `native`, `credit_alphanum4`, or `credit_alphanum12`.

* buying\_asset\_issuer `string`

  The Stellar address of the buying asset’s issuer. Appears if the `buying_asset_type` is not `native`.

* buying\_asset\_code `string`

  The code for the buying asset. Appears if the `buying_asset_type` is not `native`.

* selling\_asset\_type `string`

  The type for the selling asset. Either `native`, `credit_alphanum4`, or `credit_alphanum12`.

* selling\_asset\_issuer `string`

  The Stellar address of the selling asset’s issuer. Appears if the `selling_asset_type` is not `native`.

* selling\_asset\_code `string`

  The code for the selling asset. Appears if the `selling_asset_type` is not `native`.

* offer\_id `string`

  A unique identifier for this offer.

```bash
{
  "_links": {
    "self": {
      "href": "https://expansion-testnet.bantu.network/operations/124893981065674756"
    },
    "transaction": {
      "href": "https://expansion-testnet.bantu.network/transactions/3b41ec1411ed67ed47c96c34067c9fcfadf6e7cc013effa0b10f3df5ed758ffc"
    },
    "effects": {
      "href": "https://expansion-testnet.bantu.network/operations/124893981065674756/effects"
    },
    "succeeds": {
      "href": "https://expansion-testnet.bantu.network/effects?order=desc\u0026cursor=124893981065674756"
    },
    "precedes": {
      "href": "https://expansion-testnet.bantu.network/effects?order=asc\u0026cursor=124893981065674756"
    }
  },
  "id": "124893981065674756",
  "paging_token": "124893981065674756",
  "transaction_successful": true,
  "source_account": "GDT7WYNV6YBFJH3G6TX5K3ALBZY7A7A7CLIGXK4XZ6H5SROPS4UFGEMC",
  "type": "manage_buy_offer",
  "type_i": 12,
  "created_at": "2020-04-08T14:03:03Z",
  "transaction_hash": "3b41ec1411ed67ed47c96c34067c9fcfadf6e7cc013effa0b10f3df5ed758ffc",
  "amount": "20.4521401",
  "price": "0.0300003",
  "price_r": {
    "n": 9000190,
    "d": 300003333
  },
  "buying_asset_type": "native",
  "selling_asset_type": "credit_alphanum4",
  "selling_asset_code": "EURT",
  "selling_asset_issuer": "GAP5LETOV6YIE62YAM56STDANPRDO7ZFDBGSNHJQIYGGKSMOZAHOOS2S",
  "offer_id": "0"
}
```

