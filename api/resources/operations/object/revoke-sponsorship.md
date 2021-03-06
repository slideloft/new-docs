---
title: Revoke Sponsorship
order: 190
---

# Revoke Sponsorship

Revoke sponsorship of a ledger entry.

 - ATTRIBUTE -

* account\_id `string (optional)`

  The id of the account which is no longer sponsored.

* claimable\_balance\_id `string (optional)`

  The id of the claimable balance which is no longer sponsored.

* data\_account\_id `string (optional)`

  The id of the account whose data entry is no longer sponsored.

* data\_name `string (optional)`

  The name of the data entry which is no longer sponsored.

* offer\_id `string (optional)`

  The id of the offer which is no longer sponsored.

* trustline\_account\_id `string (optional)`

  The id of the account whose trustline is no longer sponsored.

* trustline\_asset `string (optional)`

  The asset of the trustline which is no longer sponsored.

* signer\_account\_id `string (optional)`

  The account id of the signer which is no longer sponsored.

* signer\_key `string (optional)`

  The type of the signer which is no longer sponsored.

```bash
{
  "_links": {
    "self": {
      "href": "https://horizon.stellar.org/operations/124922916260433921"
    },
    "transaction": {
      "href": "https://horizon.stellar.org/transactions/f94c338370839a598753221714de0b0193d4fc56ea369db6efe88f18669cc5a1"
    },
    "effects": {
      "href": "https://horizon.stellar.org/operations/124922916260433921/effects"
    },
    "succeeds": {
      "href": "https://horizon.stellar.org/effects?order=desc\u0026cursor=124922916260433921"
    },
    "precedes": {
      "href": "https://horizon.stellar.org/effects?order=asc\u0026cursor=124922916260433921"
    }
  },
  "id": "124922916260433921",
  "paging_token": "124922916260433921",
  "transaction_successful": true,
  "source_account": "GAYOLLLUIZE4DZMBB2ZBKGBUBZLIOYU6XFLW37GBP2VZD3ABNXCW4BVA",
  "type": "revoke_sponsorship",
  "type_i": 19,
  "created_at": "2020-04-09T00:14:11Z",
  "transaction_hash": "f94c338370839a598753221714de0b0193d4fc56ea369db6efe88f18669cc5a1",
  "account_id": "GAYOLLLUIZE4DZMBB2ZBKGBUBZLIOYU6XFLW37GBP2VZD3ABNXCW4BVA"
}
```

