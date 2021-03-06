---
title: Change Trust Object
order: 90
---

# Change Trust

Creates, updates, or deletes a trust line from the source account to another account's issued asset.

See the [`Change Trust` errors](../../../errors/result-codes/operation-specific/change-trust.md).

 - ATTRIBUTE - 

* asset\_type `string`

  The type of asset being trusted. Either `native`, `credit_alphanum4`, or `credit_alphanum12`.

* asset\_code `string`

  The Stellar address of the asset being trusted.

* asset\_issuer `string`

  The code for the asset being trusted.

* limit `string`

  Limits the amount of an asset that the source account can hold.

* trustee `string`

  The issuing account.

* trustor `string`

  The source account

```bash
{
  "_links": {
    "self": {
      "href": "https://expansion-testnet.bantu.network/operations/120192477935251457"
    },
    "transaction": {
      "href": "https://expansion-testnet.bantu.network/transactions/ec4116595bdfa8c1039c40af425e497c91fcf387c2a2a0cfa1f3bf64733f1f23"
    },
    "effects": {
      "href": "https://expansion-testnet.bantu.network/operations/120192477935251457/effects"
    },
    "succeeds": {
      "href": "https://expansion-testnet.bantu.network/effects?order=desc\u0026cursor=120192477935251457"
    },
    "precedes": {
      "href": "https://expansion-testnet.bantu.network/effects?order=asc\u0026cursor=120192477935251457"
    }
  },
  "id": "120192477935251457",
  "paging_token": "120192477935251457",
  "transaction_successful": true,
  "source_account": "GAYOLLLUIZE4DZMBB2ZBKGBUBZLIOYU6XFLW37GBP2VZD3ABNXCW4BVA",
  "type": "change_trust",
  "type_i": 6,
  "created_at": "2020-01-29T19:46:55Z",
  "transaction_hash": "ec4116595bdfa8c1039c40af425e497c91fcf387c2a2a0cfa1f3bf64733f1f23",
  "asset_type": "credit_alphanum4",
  "asset_code": "NGNT",
  "asset_issuer": "GAWODAROMJ33V5YDFY3NPYTHVYQG7MJXVJ2ND3AOGIHYRWINES6ACCPD",
  "limit": "922337203685.4775807",
  "trustee": "GAWODAROMJ33V5YDFY3NPYTHVYQG7MJXVJ2ND3AOGIHYRWINES6ACCPD",
  "trustor": "GAYOLLLUIZE4DZMBB2ZBKGBUBZLIOYU6XFLW37GBP2VZD3ABNXCW4BVA"
}
```

