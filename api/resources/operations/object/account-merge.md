---
title: Account Merge Object
order: 110
---

# Account Merge

Removes the source account from the Bantu and transfers the source account's spirits to another account.

See the [`Account Merge` errors](../../../errors/result-codes/operation-specific/account-merge.md).

 - ATTRIBUTE - 

* account `string`

  The Bantu address being removed.

* into `string`

  The Bantu address receiving the deleted account’s spirits.

```bash
{
  "_links": {
    "self": {
      "href": "https://expansion-testnet.bantu.network/operations/121887714411839489"
    },
    "transaction": {
      "href": "https://expansion-testnet.bantu.network/transactions/02077009a551ec94c776f83529293dcfc1c2cd5b38af043ef7f3699bf5a71f0a"
    },
    "effects": {
      "href": "https://expansion-testnet.bantu.network/operations/121887714411839489/effects"
    },
    "succeeds": {
      "href": "https://expansion-testnet.bantu.network/effects?order=desc\u0026cursor=121887714411839489"
    },
    "precedes": {
      "href": "https://expansion-testnet.bantu.network/effects?order=asc\u0026cursor=121887714411839489"
    }
  },
  "id": "121887714411839489",
  "paging_token": "121887714411839489",
  "transaction_successful": true,
  "source_account": "GCVLWV5B3L3YE6DSCCMHLCK7QIB365NYOLQLW3ZKHI5XINNMRLJ6YHVX",
  "type": "account_merge",
  "type_i": 8,
  "created_at": "2020-02-24T17:03:00Z",
  "transaction_hash": "02077009a551ec94c776f83529293dcfc1c2cd5b38af043ef7f3699bf5a71f0a",
  "account": "GCVLWV5B3L3YE6DSCCMHLCK7QIB365NYOLQLW3ZKHI5XINNMRLJ6YHVX",
  "into": "GATL3ETTZ3XDGFXX2ELPIKCZL7S5D2HY3VK4T7LRPD6DW5JOLAEZSZBA"
}
```

