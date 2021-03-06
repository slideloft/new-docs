---
title: Retrieve a Claimable Balance
order: 20
---

# Single

The single claimable balance endpoint provides information on a claimable balance.

 - ARGUMENT - 

* claimable\_balance\_id `required`

  A unique identifier for this claimable balance.

{% tabs %}
{% tab title="JavaScript" %}
```javascript
var StellarSdk = require("stellar-sdk");
var server = new StellarSdk.Server("https://expansion-testnet.bantu.network");

server
  .claimableBalances()
  .claimableBalanceId(
    "000000000102030000000000000000000000000000000000000000000000000000000000",
  )
  .call()
  .then(function (resp) {
    console.log(resp);
  })
  .catch(function (err) {
    console.error(err);
  });
```
{% endtab %}

{% tab title="cURL" %}
```bash
curl "https://expansion-testnet.bantu.network/claimable_balances/000000000102030000000000000000000000000000000000000000000000000000000000"
```
{% endtab %}
{% endtabs %}

```bash
{
  "_links": {
    "self": {
      "href": "https://expansion-testnet.bantu.network/claimable_balances/000000000102030000000000000000000000000000000000000000000000000000000000"
    }
  },
  "id": "000000000102030000000000000000000000000000000000000000000000000000000000",
  "paging_token": "000000000102030000000000000000000000000000000000000000000000000000000000",
  "asset": "native",
  "amount": "10.0000000",
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
  ],
  "last_modified_ledger": 28411995,
  "last_modified_time": "2020-02-26T19:29:16Z"
}
```

