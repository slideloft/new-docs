---
title: Create Claimable Balance
order: 140
---

# Create Claimable Balance

Creates a new claimable balance.

 - ATTRIBUTE - 



* asset `string`

  The asset available to be claimed in the [SEP-11 form](https://github.com/stellar/stellar-protocol/blob/0c675fb3a482183dcf0f5db79c12685acf82a95c/ecosystem/sep-0011.md#values) `asset_code:issuing_address` or `native` \(for XLM\)

* amount `string`

  The amount available to be claimed.

* claimants `array of objects`

  The list of entries which could claim the claimable balance.Hide child attributes

  * destination `string`

    The account ID who can claim the balance.

  * predicate `object`

    The condition which must be satisfied so `destination` can claim the balance.Hide child attributes

    * unconditional `boolean (optional)`

      If true it means this clause of the condition is always satisfied.

    * and `array of objects (optional)`

      The array will always contain two elements which also are predicates. This clause of the condition is satisfied if both of the two elements in the array are satisfied.

    * or `array of objects (optional)`

      The array will always contain two elements which also are predicates. This clause of the condition is satisfied if at least one of the two elements in the array are satisfied.

    * notobject \(optional\)

      The value is also a predicate. This clause of the condition is satisfied if the value is _not_ satisfied.

    * absBeforestring \(optional\)

      An ISO 8601 formatted string representing a deadline for when the claimable balance can be claimed. If the balance is claimed before the date then this clause of the condition is satisfied.

    * relBeforestring \(optional\)

      A relative deadline for when the claimable balance can be claimed. The value represents the number of seconds since the close time of the ledger which created the claimable balance.

```bash
{
  "_links": {
    "self": {
      "href": "https://expansion-testnet.bantu.network/operations/124922916260433921"
    },
    "transaction": {
      "href": "https://expansion-testnet.bantu.network/transactions/f94c338370839a598753221714de0b0193d4fc56ea369db6efe88f18669cc5a1"
    },
    "effects": {
      "href": "https://expansion-testnet.bantu.network/operations/124922916260433921/effects"
    },
    "succeeds": {
      "href": "https://expansion-testnet.bantu.network/effects?order=desc\u0026cursor=124922916260433921"
    },
    "precedes": {
      "href": "https://expansion-testnet.bantu.network/effects?order=asc\u0026cursor=124922916260433921"
    }
  },
  "id": "124922916260433921",
  "paging_token": "124922916260433921",
  "transaction_successful": true,
  "source_account": "GAYOLLLUIZE4DZMBB2ZBKGBUBZLIOYU6XFLW37GBP2VZD3ABNXCW4BVA",
  "type": "create_claimable_balance",
  "type_i": 14,
  "created_at": "2020-04-09T00:14:11Z",
  "transaction_hash": "f94c338370839a598753221714de0b0193d4fc56ea369db6efe88f18669cc5a1",
  "asset": "NGNT:GAWODAROMJ33V5YDFY3NPYTHVYQG7MJXVJ2ND3AOGIHYRWINES6ACCPD",
  "amount": "200.0000000",
  "claimants": [
    {
      "destination": "GC3C4AKRBQLHOJ45U4XG35ESVWRDECWO5XLDGYADO6DPR3L7KIDVUMML",
      "predicate": {
        {
          "and": [
            {
              "or": [
                {
                  "relBefore": "12"
                },
                {
                  "absBefore": "2020-08-26T11:15:39Z"
                }
              ]
            },
            {
              "not": {"unconditional": true}
            }
          ]
        }
      }
    }
  ]
}
```

