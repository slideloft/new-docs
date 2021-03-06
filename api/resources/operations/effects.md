---
title: Retrieve an Operation's Effects
order: 30
---

# Effects

This endpoint returns the effects of a specific operation.

 - ARGUMENT - 

* id `required`

  The ID number for this operation.

* cursor `optional`

  A number that points to a specific location in a collection of responses and is pulled from the `paging_token` value of a record.

* order `optional`

  A designation of the order in which records should appear. Options include `asc`\(ascending\) or `desc` \(descending\). If this argument isn’t set, it defaults to `asc`.

* limit `optional`

  The total number of records returned. The limit can range from 1 to 200 - an upper limit that is hardcoded in Horizon for performance reasons. If this argument isn’t designated, it defaults to 10.

{% tabs %}
{% tab title="JavaScript" %}
```javascript
var StellarSdk = require("stellar-sdk");
var server = new StellarSdk.Server("https://expansion-testnet.bantu.network");

server
  .effects()
  .forOperation("121693057904021505")
  .call()
  .then(function (resp) {
    console.log(resp);
  })
  .catch(function (err) {
    console.error(err);
  });
```
{% endtab %}

{% tab title="" %}
```
curl "https://expansion-testnet.bantu.network/operations/121693057904021505/effects"
```
{% endtab %}
{% endtabs %}

```bash
{
  "_links": {
    "self": {
      "href": "https://expansion-testnet.bantu.network/operations/121693057904021505/effects?cursor=\u0026limit=10\u0026order=asc"
    },
    "next": {
      "href": "https://expansion-testnet.bantu.network/operations/121693057904021505/effects?cursor=121693057904021505-2\u0026limit=10\u0026order=asc"
    },
    "prev": {
      "href": "https://expansion-testnet.bantu.network/operations/121693057904021505/effects?cursor=121693057904021505-1\u0026limit=10\u0026order=desc"
    }
  },
  "_embedded": {
    "records": [
      {
        "_links": {
          "operation": {
            "href": "https://expansion-testnet.bantu.network/operations/121693057904021505"
          },
          "succeeds": {
            "href": "https://expansion-testnet.bantu.network/effects?order=desc\u0026cursor=121693057904021505-1"
          },
          "precedes": {
            "href": "https://expansion-testnet.bantu.network/effects?order=asc\u0026cursor=121693057904021505-1"
          }
        },
        "id": "0121693057904021505-0000000001",
        "paging_token": "121693057904021505-1",
        "account": "GALSPNVKGNRJ3VIOQ26QKPZBDCTVJK7XPLSPF3UVZV3JJXCKVCHNSPCK",
        "type": "account_credited",
        "type_i": 2,
        "created_at": "2020-02-21T20:27:30Z",
        "asset_type": "credit_alphanum4",
        "asset_code": "NODL",
        "asset_issuer": "GB2Y3AWXVROM2BHFQKQPTWKIOI3TZEBBD3LTKTVQTKEPXGOBE742NODL",
        "amount": "0.0000027"
      },
      {
        "_links": {
          "operation": {
            "href": "https://expansion-testnet.bantu.network/operations/121693057904021505"
          },
          "succeeds": {
            "href": "https://expansion-testnet.bantu.network/effects?order=desc\u0026cursor=121693057904021505-2"
          },
          "precedes": {
            "href": "https://expansion-testnet.bantu.network/effects?order=asc\u0026cursor=121693057904021505-2"
          }
        },
        "id": "0121693057904021505-0000000002",
        "paging_token": "121693057904021505-2",
        "account": "GDQWI6FKB72DPOJE4CGYCFQZKRPQQIOYXRMZ5KEVGXMG6UUTGJMBCASH",
        "type": "account_debited",
        "type_i": 3,
        "created_at": "2020-02-21T20:27:30Z",
        "asset_type": "credit_alphanum4",
        "asset_code": "NODL",
        "asset_issuer": "GB2Y3AWXVROM2BHFQKQPTWKIOI3TZEBBD3LTKTVQTKEPXGOBE742NODL",
        "amount": "0.0000027"
      }
    ]
  }
}
```

