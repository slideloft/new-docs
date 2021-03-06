---
title: Create Passive Sell Offer Object
order: 70
---

# Passive Sell Offer

Creates an offer that will not consume a counter offer that exactly matches this offer. This is useful for offers meant to be 1:1 exchanges for path payments. Use Manage Sell Offer to manage this offer after using this operation to create it.

See the [`Create Passive Sell Offer` errors](../../../errors/result-codes/operation-specific/create-passive-sell-offer.md).

 - ATTRIBUTE - 



* amount `string`

  The amount of `selling_asset` that the account making this offer is willing to sell.

* price `string`

  How many units of `selling_asset` it takes to get 1 unit of `buying_asset`. A number representing the decimal form of `price_r`.

* price\_robject

  A precise representation of the buy and sell price of the assets on offer.Show child attributes

  * * 

* buying\_asset\_typestring

  The type for the buying asset. Either `native`, `credit_alphanum4`, or `credit_alphanum12`.

* buying\_asset\_issuerstring

  The Stellar address of the buying asset’s issuer. Appears if the `buying_asset_type` is not `native`.

* buying\_asset\_codestring

  The code for the buying asset. Appears if the `buying_asset_type` is not `native`.

* selling\_asset\_typestring

  The type for the selling asset. Either `native`, `credit_alphanum4`, or `credit_alphanum12`.

* selling\_asset\_issuerstring

  The Stellar address of the selling asset’s issuer. Appears if the `selling_asset_type` is not `native`.

* selling\_asset\_codestring

  The code for the selling asset. Appears if the `selling_asset_type` is not `native`.

* offer\_idstring

  A unique identifier for this offer.

```bash
{
  "_links": {
    "self": {
      "href": "https://expansion-testnet.bantu.network/operations/124895183656849409"
    },
    "transaction": {
      "href": "https://expansion-testnet.bantu.network/transactions/20afb7f9613efe9e851579190c80758ee101550e85740f71274c3eb3f0cb0418"
    },
    "effects": {
      "href": "https://expansion-testnet.bantu.network/operations/124895183656849409/effects"
    },
    "succeeds": {
      "href": "https://expansion-testnet.bantu.network/effects?order=desc\u0026cursor=124895183656849409"
    },
    "precedes": {
      "href": "https://expansion-testnet.bantu.network/effects?order=asc\u0026cursor=124895183656849409"
    }
  },
  "id": "124895183656849409",
  "paging_token": "124895183656849409",
  "transaction_successful": true,
  "source_account": "GAYOLLLUIZE4DZMBB2ZBKGBUBZLIOYU6XFLW37GBP2VZD3ABNXCW4BVA",
  "type": "create_passive_sell_offer",
  "type_i": 4,
  "created_at": "2020-04-08T14:28:15Z",
  "transaction_hash": "20afb7f9613efe9e851579190c80758ee101550e85740f71274c3eb3f0cb0418",
  "amount": "1.0000000",
  "price": "1.0000000",
  "price_r": {
    "n": 1,
    "d": 1
  },
  "buying_asset_type": "credit_alphanum4",
  "buying_asset_code": "USD",
  "buying_asset_issuer": "GBNLJIYH34UWO5YZFA3A3HD3N76R6DOI33N4JONUOHEEYZYCAYTEJ5AK",
  "selling_asset_type": "credit_alphanum4",
  "selling_asset_code": "USD",
  "selling_asset_issuer": "GDUKMGUGDZQK6YHYA5Z6AY2G4XDSZPSZ3SW5UN3ARVMO6QSRDWP5YLEX"
}
```

