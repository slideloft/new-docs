---
title: Retrieve a Ledgers's Effects
order: 50
---

# Effects

This endpoint returns the effects of a specific ledger.

{% tabs %}
{% tab title="JavaScript" %}
```javascript
var StellarSdk = require("stellar-sdk");
var server = new StellarSdk.Server("https://expansion-testnet.bantu.network");

server
  .effects()
  .forLedger(0)
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
curl "https://expansion-testnet.bantu.network/ledgers/0/effects"
```
{% endtab %}
{% endtabs %}

```bash
{
  "_links": {
    "self": {
      "href": "https://expansion-testnet.bantu.network/ledgers/0/effects?cursor=&limit=10&order=asc"
    },
    "next": {
      "href": "https://horizon.stellar.org/ledgers/0/effects?cursor=33676838572034-1&limit=10&order=asc"
    },
    "prev": {
      "href": "https://expansion-testnet.bantu.network/ledgers/0/effects?cursor=12884905985-1&limit=10&order=desc"
    }
  },
  "_embedded": {
    "records": [
      {
        "_links": {
          "operation": {
            "href": "https://expansion-testnet.bantu.network/operations/12884905985"
          },
          "succeeds": {
            "href": "https://expansion-testnet.bantu.network/effects?order=desc&cursor=12884905985-1"
          },
          "precedes": {
            "href": "https://expansion-testnet.bantu.network/effects?order=asc&cursor=12884905985-1"
          }
        },
        "id": "0000000012884905985-0000000001",
        "paging_token": "12884905985-1",
        "account": "GALPCCZN4YXA3YMJHKL6CVIECKPLJJCTVMSNYWBTKJW4K5HQLYLDMZTB",
        "type": "account_created",
        "type_i": 0,
        "created_at": "2015-09-30T17:15:54Z",
        "starting_balance": "20.0000000"
      },
      {
        "_links": {
          "operation": {
            "href": "https://expansion-testnet.bantu.network//operations/12884905985"
          },
          "succeeds": {
            "href": "https://expansion-testnet.bantu.network/effects?order=desc&cursor=12884905985-2"
          },
          "precedes": {
            "href": "https://expansion-testnet.bantu.network/effects?order=asc&cursor=12884905985-2"
          }
        },
        "id": "0000000012884905985-0000000002",
        "paging_token": "12884905985-2",
        "account": "GAAZI4TCR3TY5OJHCTJC2A4QSY6CJWJH5IAJTGKIN2ER7LBNVKOCCWN7",
        "type": "account_debited",
        "type_i": 3,
        "created_at": "2015-09-30T17:15:54Z",
        "asset_type": "native",
        "amount": "20.0000000"
      }
    ]
  }
}
```

