---
title: List All Transactions
order: 50
---

# List

This endpoint lists all successful transactions and can be used in [streaming](../../introduction/streaming.md) mode. Streaming mode allows you to listen for new transactions as they are added to the Stellar ledger. If called in streaming mode, Horizon will start at the earliest known transaction unless a `cursor` is set, in which case it will start from that `cursor`. By setting the cursor value to `now`, you can stream transactions created since your request time.

 - ARGUMENT - 

* transaction\_hash `required`

  A hex-encoded SHA-256 hash of this transaction’s XDR-encoded form.

* cursoroptional

  A number that points to a specific location in a collection of responses and is pulled from the `paging_token` value of a record.

* order `optional`

  A designation of the order in which records should appear. Options include `asc`\(ascending\) or `desc` \(descending\). If this argument isn’t set, it defaults to `asc`.

* limit `optional`

  The total number of records returned. The limit can range from 1 to 200 - an upper limit that is hardcoded in Horizon for performance reasons. If this argument isn’t designated, it defaults to 10.

{% tabs %}
{% tab title="JavaScript" %}
```javascript
var StellarSdk = require("stellar-sdk");
var server = new StellarSdk.Server("https://horizon.stellar.org");

server
  .effects()
  .forTransaction(
    "512a9946bc7ff4a363299f14f79e0beb9b9cdbd0103e3a69a44446a0aa6471a8",
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
curl "https://expansion-testnet.bantu.network/transactions/512a9946bc7ff4a363299f14f79e0beb9b9cdbd0103e3a69a44446a0aa6471a8/effects"
```
{% endtab %}
{% endtabs %}

```bash
{
  "_links": {
    "self": {
      "href": "https://expansion-testnet.bantu.network/transactions/512a9946bc7ff4a363299f14f79e0beb9b9cdbd0103e3a69a44446a0aa6471a8/effects?cursor=\u0026limit=10\u0026order=asc"
    },
    "next": {
      "href": "https://expansion-testnet.bantu.network/transactions/512a9946bc7ff4a363299f14f79e0beb9b9cdbd0103e3a69a44446a0aa6471a8/effects?cursor=121628667754319873-2\u0026limit=10\u0026order=asc"
    },
    "prev": {
      "href": "https://expansion-testnet.bantu.network/transactions/512a9946bc7ff4a363299f14f79e0beb9b9cdbd0103e3a69a44446a0aa6471a8/effects?cursor=121628667754319873-1\u0026limit=10\u0026order=desc"
    }
  },
  "_embedded": {
    "records": [
      {
        "_links": {
          "operation": {
            "href": "https://expansion-testnet.bantu.network/operations/121628667754319873"
          },
          "succeeds": {
            "href": "https://expansion-testnet.bantu.network/effects?order=desc\u0026cursor=121628667754319873-1"
          },
          "precedes": {
            "href": "https://expansion-testnet.bantu.network/effects?order=asc\u0026cursor=121628667754319873-1"
          }
        },
        "id": "0121628667754319873-0000000001",
        "paging_token": "121628667754319873-1",
        "account": "GAHK7EEG2WWHVKDNT4CEQFZGKF2LGDSW2IVM4S5DP42RBW3K6BTODB4A",
        "type": "account_credited",
        "type_i": 2,
        "created_at": "2020-02-20T21:18:33Z",
        "asset_type": "native",
        "amount": "1573.5112616"
      },
      {
        "_links": {
          "operation": {
            "href": "https://expansion-testnet.bantu.network/operations/121628667754319873"
          },
          "succeeds": {
            "href": "https://expansion-testnet.bantu.network/effects?order=desc\u0026cursor=121628667754319873-2"
          },
          "precedes": {
            "href": "https://expansion-testnet.bantu.network/effects?order=asc\u0026cursor=121628667754319873-2"
          }
        },
        "id": "0121628667754319873-0000000002",
        "paging_token": "121628667754319873-2",
        "account": "GA2XP4KMY4KWNPW4KUCUKYUF2J7Y6HO5HLPUEA3VPVSMYCM3TGNEZP5S",
        "type": "account_debited",
        "type_i": 3,
        "created_at": "2020-02-20T21:18:33Z",
        "asset_type": "native",
        "amount": "1573.5112616"
      }
    ]
  }
}
```

```bash
var StellarSdk = require("stellar-sdk");
var server = new StellarSdk.Server("https://expansion-testnet.bantu.network");

var tradesHandler = function (resp) {
  console.log(resp);
};

var es = server
  .transactions()
  .cursor("now")
  .stream({ onmessage: tradesHandler });
```

