---
title: Create Account Object
order: 10
---

# Create Account

Creates and funds a new account with the specified starting balance.

See the [`Create Account` errors](../../../errors/result-codes/operation-specific/create-account.md).

 ATTRIBUTE 

* starting\_balance `string`

  The amount of XLM to send the newly created account.

* funder `string`

  The account that funds the new account.

* account `string`

  A new account that is funded.

```bash
{
  "_links": {
    "self": {
      "href": "https://expansion-testnet.bantu.network/operations/120192344791343105"
    },
    "transaction": {
      "href": "https://expansion-testnet.bantu.network/transactions/ef0fe04ac3c7de7228ca2598886059868ad05c224a041e8b2d9ee2a8a9dd6894"
    },
    "effects": {
      "href": "https://expansion-testnet.bantu.network/operations/120192344791343105/effects"
    },
    "succeeds": {
      "href": "https://expansion-testnet.bantu.network/effects?order=desc\u0026cursor=120192344791343105"
    },
    "precedes": {
      "href": "https://expansion-testnet.bantu.network/effects?order=asc\u0026cursor=120192344791343105"
    }
  },
  "id": "120192344791343105",
  "paging_token": "120192344791343105",
  "transaction_successful": true,
  "source_account": "GBVFTZL5HIPT4PFQVTZVIWR77V7LWYCXU4CLYWWHHOEXB64XPG5LDMTU",
  "type": "create_account",
  "type_i": 0,
  "created_at": "2020-01-29T19:43:59Z",
  "transaction_hash": "ef0fe04ac3c7de7228ca2598886059868ad05c224a041e8b2d9ee2a8a9dd6894",
  "starting_balance": "2.0000000",
  "funder": "GBVFTZL5HIPT4PFQVTZVIWR77V7LWYCXU4CLYWWHHOEXB64XPG5LDMTU",
  "account": "GAYOLLLUIZE4DZMBB2ZBKGBUBZLIOYU6XFLW37GBP2VZD3ABNXCW4BVA"
}
```

