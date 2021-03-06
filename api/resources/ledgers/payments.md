---
title: Retrieve a Ledger's Payments
order: 40
---

# Payments

This endpoint returns all payment-related operations in a specific ledger.

Operation types that can be returned by this endpoint include:

* `create_account`
* `payment`
* `path_payment`
* `account_merge`

{% tabs %}
{% tab title="JavaScript" %}
```javascript
var StellarSdk = require("stellar-sdk");
var server = new StellarSdk.Server("https://expansion-testnet.bantu.network/");

server
  .payments()
  .forLedger("27521176")
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
curl "https://expansion-testnet.bantu.network/ledgers/27521176/payments?limit=1"
```
{% endtab %}
{% endtabs %}

```bash
{
  "_links": {
    "self": {
      "href": "https://expansion-testnet.bantu.network/ledgers/27521176/payments?cursor=\u0026limit=1\u0026order=asc"
    },
    "next": {
      "href": "https://expansion-testnet.bantu.network/ledgers/27521176/payments?cursor=118202550867476481\u0026limit=1\u0026order=asc"
    },
    "prev": {
      "href": "https://expansion-testnet.bantu.network/ledgers/27521176/payments?cursor=118202550867476481\u0026limit=1\u0026order=desc"
    }
  },
  "_embedded": {
    "records": [
      {
        "_links": {
          "self": {
            "href": "https://expansion-testnet.bantu.network/operations/118202550867476481"
          },
          "transaction": {
            "href": "https://expansion-testnet.bantu.network/transactions/971454b84a82baa38afa975e9eb4ff2632821b5a3e7f7993a7e20bbd9d7633ea"
          },
          "effects": {
            "href": "https://expansion-testnet.bantu.network/operations/118202550867476481/effects"
          },
          "succeeds": {
            "href": "https://expansion-testnet.bantu.network/effects?order=desc\u0026cursor=118202550867476481"
          },
          "precedes": {
            "href": "https://expansion-testnet.bantu.network/effects?order=asc\u0026cursor=118202550867476481"
          }
        },
        "id": "118202550867476481",
        "paging_token": "118202550867476481",
        "transaction_successful": true,
        "source_account": "GDQWI6FKB72DPOJE4CGYCFQZKRPQQIOYXRMZ5KEVGXMG6UUTGJMBCASH",
        "type": "payment",
        "type_i": 1,
        "created_at": "2019-12-30T22:35:49Z",
        "transaction_hash": "971454b84a82baa38afa975e9eb4ff2632821b5a3e7f7993a7e20bbd9d7633ea",
        "asset_type": "credit_alphanum4",
        "asset_code": "NODL",
        "asset_issuer": "GB2Y3AWXVROM2BHFQKQPTWKIOI3TZEBBD3LTKTVQTKEPXGOBE742NODL",
        "from": "GDQWI6FKB72DPOJE4CGYCFQZKRPQQIOYXRMZ5KEVGXMG6UUTGJMBCASH",
        "to": "GDGJS7AXAUFDZARIRDVZ5V7CFW6XY47WSBE2OVLCCGCDWOE7INKYN3PS",
        "amount": "0.0000017"
      }
    ]
  }
}
```

