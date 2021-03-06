---
title: The Trade Object
order: 10
---

# Object

import { ExampleResponse } from "components/ExampleResponse"; import { AttributeTable } from "components/AttributeTable";

When Horizon returns information about a trade, it uses the following format:

 - ATTRIBUTE - 

* id `string`

  A unique identifier for this trade.

* paging\_token `number`

  A cursor value for use in [pagination](https://developers.stellar.org/api/introduction/pagination/).

* ledger\_close\_time `string`

  An ISO 8601 formatted string of when the ledger with this trade was closed.

* offer\_id `string`

  The sell offer ID. **DECPRECATED**

* base\_account `string`

  The account ID of the base party for this trade.

* base\_offer\_id `string`

  The base offer ID. If this offer was immediately and fully consumed, this will be a synethic ID.

* base\_amount `string`

  The amount of the base asset that was moved from `base_account` to `counter_account`.

* base\_asset\_type `string`

  The type for the base asset. Either `native`, `credit_alphanum4`, or `credit_alphanum12`.

* base\_asset\_code `string`

  The code for the base asset.

* base\_asset\_issuer `string`

  The Stellar address of the base asset’s issuer.

* counter\_offer\_id `string`

  The counter offer ID. If this offer was immediately and fully consumed, this will be a synethic ID.

* counter\_amount `string`

  The amount of the counter asset that was moved from `counter_account` to `base_account`.

* counter\_asset\_type `string`

  The type for the counter asset. Either `native`, `credit_alphanum4`, or `credit_alphanum12`.

* counter\_asset\_code `string`

  The code for the counter asset.

* counter\_asset\_issuer `string`

  The Stellar address of the counter asset’s issuer.

* price `object`

  An object of a number numerator and number denominator that represents the original offer price. To derive the price, divide `n` by `d`.Hide child attributes

  * nnumber

    The numerator.

  * dnumber

    The denominator.

* base\_is\_seller `boolean`

  Indicates with party is the seller.

```bash
{
  "_links": {
    "self": {
      "href": ""
    },
    "base": {
      "href": "https://expansion-testnet.bantu.network/accounts/GA23DVJUJVXUQ45SKQMZR7KH2ZOOBFWGWSEXHCT7VVKP2TYIMCQTQGNQ"
    },
    "counter": {
      "href": "https://expansion-testnet.bantu.network/accounts/GAFGG7CRFRCJLBHGI5L4IZD4QYR4GDX5NKB46CE4KZMNBILBTP3L4M75"
    },
    "operation": {
      "href": "https://expansion-testnet.bantu.network/operations/100089067462524929"
    }
  },
  "id": "100089067462524929-0",
  "paging_token": "100089067462524929-0",
  "ledger_close_time": "2019-04-07T11:30:03Z",
  "offer_id": "79502917",
  "base_offer_id": "4711775085889912833",
  "base_account": "GA23DVJUJVXUQ45SKQMZR7KH2ZOOBFWGWSEXHCT7VVKP2TYIMCQTQGNQ",
  "base_amount": "99.9999996",
  "base_asset_type": "native",
  "counter_offer_id": "79502917",
  "counter_account": "GAFGG7CRFRCJLBHGI5L4IZD4QYR4GDX5NKB46CE4KZMNBILBTP3L4M75",
  "counter_amount": "11.4722884",
  "counter_asset_type": "credit_alphanum4",
  "counter_asset_code": "EURT",
  "counter_asset_issuer": "GAP5LETOV6YIE62YAM56STDANPRDO7ZFDBGSNHJQIYGGKSMOZAHOOS2S",
  "base_is_seller": false,
  "price": {
    "n": 10000000,
    "d": 87166567
  }
}
```

